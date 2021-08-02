# Could We Replace Our Journalists With an AI?

As with so many bits of discovery I end up doing, this all started with a flippant conversation with a colleague...

![AI journalist](/assets/images/ai-journalist.jpeg)

## A Bit of Background
I've recently been working with one of our teams on migrating them to a new Content Management System, and as part of that I've ended up becoming much more familiar with their content than I previously had been. Being a natural pattern-matcher, I started to notice trends not just in the theme of the content, but also in the structure and the editorial style. These are deliberate and carefully curated editorial decisions taken by experienced journalists, but I did start to wonder out loud if you could feed these decisions into an AI and use it to generate content that would be indistinguishable from the content created by our human journalists.

Having started as a bit of a joke, it really got me thinking, so I decided to do a bit of digging.

## Disclaimer
This is obviously just a bit of fun, and I'm not for one second suggesting that the hard-working and talented editorial teams at LADbible Group could be replaced by a crudely-tuned neural network. These teams create articles every day that are consistently some of the most engaging content on the internet, which is reflected in the success of LADbible's various brands, and as clever as AI is, it still doesn't come close to achieving what they manage to do every single day.

## GPT-2
We've all seen the "we fed such-and-such into an AI and this is what it produced" stuff online, but what is the AI, and how does it work? After some well-placed Google searches, I found [GPT-2](https://openai.com/blog/better-language-models/). It's an open-sourced neural network created by [OpenAI](https://openai.com/), that is designed to "simply" predict the next word after being given 40GB of text from the internet.

I was interested to find out how they selected the text from the internet, and it turns out that they scraped web pages that had been linked to from Reddit, where the link had received at least 3 up-votes. Internet crowd-sourcing at it's absolute finest.

If you want to know more about GPT-2, I'd strongly recommend having a read of [this](https://jalammar.github.io/illustrated-gpt2/) excellent blog post.

## gpt-2-simple
Ok so I know there's a model out there that could be tuned to achieve my objective, but how do I actually use it? I'm no data scientist, and I'm not familiar with the tools that they use, but fortunately someone had done, and open-sourced, a lot of the work for me. The excellent [gpt-2-simple](https://jalammar.github.io/illustrated-gpt2/) library was the tool that I needed.

It provides helper functions for downloading the core model, tuning it using your own data, and then generating some text based on it.

Also, it's a Python library, which is great for all the Python developers. Which I'm not.

## Writing some Python
It was clear at this point I was going to have to bite the bullet and write some Python. The process would look something like this:

1. Use the LADbible content API to download the title and body of 500 articles from one of LADbible Group's websites, namely [Tyla.com](https://www.tyla.com)
1. Strip the HTML from the body, leaving only the text, and then write all of that data to a text file
1. Download the `124M` GPT-2 core model
1. Re-tune the model using the data from our API
1. Marvel at the results

Apologies to any Python developers reading this, but I had to piece together Python code from examples in the `gpt-2-simple` GitHub README, and code I'd pinched from Stack Overflow. Here's what I came up with:

```python
import gpt_2_simple as gpt2
import os
import json
import re

model_name = "124M"
if not os.path.isdir(os.path.join("models", model_name)):
  print('Downloading model...')
  gpt2.download_gpt2(model_name=model_name)   # model is saved into current directory under /models/124M/

data_json = "data.json"
with open(data_json) as jsonFile:
  jsonObject = json.load(jsonFile)
  jsonFile.close()

articleArray = jsonObject['data']['articles']#
for article in articleArray:
  body = re.sub('<[^<]+?>', '', article['body'])
  with open('rawdata.txt', 'a') as dataFile:
    dataFile.write(article['title'] + '\n')
    dataFile.write(body + '\n')
    dataFile.close()

file_name = "rawdata.txt"
sess = gpt2.start_tf_sess()
gpt2.finetune(sess,
              file_name,
              model_name=model_name,
              steps=1000)   # steps is max number of training steps

gpt2.generate(sess)
```

So now all I need to do is run it...

## It Doesn't Work On *My* Machine
So I installed the `gpt-2-simple` package using `pip3` and ran the `main.py` file using `python3`. It failed pretty much straight away, saying a `tensorflow` package was missing. So I installed that, and then it said that `tensorflow.contrib` was missing. But I couldn't install `tensorflow.contrib` using `pip3`. Frustrating.

I checked the issues in the `gpt-2-simple` repo, and it turned out that the library [didn't work using Python 3.8 onwards](https://github.com/minimaxir/gpt-2-simple/issues/269), and I was on Python 3.9. I installed `pyenv` and used that to attempt to downgrade Python to 3.7. However, I couldn't install one of the older versions due to the version of MacOS I'm using. So at this point, I was stuck.

## Docker to the Rescue
I suddenly remembered that these kind of dev machine build issues should be a thing of the past in the brave new world of containers, so I used the Python 3.6 Docker image and ran the code inside my own container. Here's what the Docker file looks like:

```dockerfile
FROM python:3.6.0

RUN mkdir -p /usr/app
COPY . /usr/app
WORKDIR /usr/app

COPY . .

RUN pip3 install gpt-2-simple tensorflow

ENTRYPOINT ["python3", "/usr/app/main.py"]
```

After building and tagging the image, the following Docker run command got the process running correctly:

```bash
docker run -v ${CURDIR}:/usr/app -it ladbibleai
```

## Tuning the Model
So after it's downloaded the "small" 124M core model (about 500MB), it starts off the tuning process, based on the provided data file. In this case, it did 1,000 iterations of training based on the data. What I hadn't expected was how long that would take - in this case, about 11 hours.

To keep things interesting, it does produce sample data at 10% increments through the training process, and you can see the AI getting more and more clever as it gets further into the tuning process.

## The Result
So here it is, in all it's glory. Some Tyla.com content, written by a machine:

> Yesterday, The Guardian revealed that Gogglebox star Liam Reardon had cancelled his tour after a female fan wrote “no more Gogglebox”.After a tumultuous six months at work, the end of Love Island and the beginning of ‘Leaving Mexico?’, it's fair to say fans have been a little less convinced about Liam's worth.The 25-year-old has made no secret of the fact he is “too smart” and “pretends like a boy to his women, friends and fans, to his small band of Secret Friends.While he may not be taking on a solo career, he's looking for work - so we at Tyla are sure he's on the lookout for work.“Liam is too smart for this world and we would love to be his match,” a source told Tyla.The new singer-up will certainly be a bit of a departure for the band, with many fans anticipating he makes another dash for the top tier of music.Marking his 50th birthday in June, fans will be keen to see whether he makes a return bound for the big screen. In a bid to find out, he uses a spectrometer on his iPad to gather complete notes for songs.“Wish I'd asked him to write those lyrics,” one fan wrote.“Heartbroken that someone could make me feel like I've betrayed them.. Wonder if that'll be okay? (Chorus: “I wrote those *marks,”” another fan wrote.&nbsp;Fans of the band will also be keen to hear that Liam is no stranger to playing dirty. He began playing the dirty in recent weeks, and will hopefully be familiar with the new lick from his former partner, Florence Shaw.Love Island&nbsp;is on weeknights at 9pm on&nbsp;ITV&nbsp;and&nbsp;ITV Hub&nbsp;. The episodes are available to stream on&nbsp;BritBox&nbsp;the following morning.Can't get enough of&nbsp;Love Island? Join our Facebook Group -&nbsp;Love Island Obsessives&nbsp;-&nbsp;and keep up to date with the latest drama.

So while some of it is pretty dodgy, gramatically speaking, and it's clearly about an event that never actually happened, it definitely _feels_ like a piece of Tyla content, so in that regard I was very impressed.

## What I'd Do Differently Next Time
Having lost far too much time to dev machine issues and then having to wait half a day to get the results, I would certainly re-assess my choice of machine.

GCP offers VM's with GPU's specifically for this kind of work, and pre-installed with all the frameworks you need, so I think that would've been a much more sensible option, rather than trying to run it all on a Macbook.

I'd also probably use a small training data-set, and perhaps just include the article body and leave out the headline.

But all in all this has been a fun foray into the world of neural networks and AI-based text generation, and I'd strongly recommend giving it a go.