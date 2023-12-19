# What I'm Looking For as a Hiring Manager

## Why I'm Writing This

The last 12 months have been a difficult year for a lot of people in tech, with very little growth and a lot of redundancies, which we haven't seen for a long time. Having seen a number of friends affected by said redundancies, I'm acutely aware of how painful this can be professionally, financially and emotionally.

Unfortunately there's very little I can do about this happening, but where I can provide some guidance is in finding another job. I've been a hiring manager for 15 years and have interviewed dozens of candidates for roles at six different businesses. Over that time, I've formed a fairly clear picture of what a "good" interview looks like, and what a candidate can do to prepare well and give themselves the best chance of success.

I'm going to caveat all of this by saying that these are just my opinions, and you might get very different opinions from other hiring managers. That being said, these are the key things that, in my view at least, you can do to prepare.

![Tech Interview](/assets/images/tech-interview.jpeg)

## Learn in Advance

There are plenty of things you can find out about before the interview happens that will give you the opportunity to demonstrate that you've "done your homework". I'm always amazed when I ask someone what they already know about the business and the role, and the answer amounts to basically nothing. Why would you go to the effort of interviewing for a business and a role that you know nothing about? Some of this is definitely down to the recruiter not preparing their candidate properly, but ultimately the responsibility is on you as the candidate to be well prepared. Some things you should definitely try and find out about are:

* The business. What's their history? What do they do? What clients/customers do they sell to? 
* The role. What are the responsibilities? What are they looking for in terms of experience and profile?
* The person interviewing you. How long have they been at the business? What were they doing before that?
* The tech stack. What frameworks are they using for front-end, middle-tier, database, cloud etc? 
* The team. Who else works there? If there's anyone you're connected with, could you speak to them and get an inside scoop on what it's really like to work there?
* The interview format. If the recruiter hasn't told you this, then tell them to find out. You need to know what you're committing yourself to before you start the process.

Why do all this? For you, it means you're getting as much information as possible before potentially making a very big decision. For your potential employer, it shows that this is a big deal for you and you're taking it seriously. Plus it shows that you're a detail-oriented person who is willing to work hard when necessary.

## Be Engaging

We spend the majority of our waking lives at work, and it's natural that we want to spend it with people we'll get on with. There are things you can do to make it clearer that you are an easy person to work with. For example, I always start an interview by asking someone how they are. I reckon the candidate asks me how I am about 50% of the time. It's these kind of micro-interactions / pleasantries that make people feel at ease.

I tend to give people a lot of information about the business and the role during an interview. It's always good when people can repeat back a summary of what I've said to confirm understanding, and/or ask me questions based on the information I've just given. It's confirmation that what I've said has sunk in.

Always prepare a few questions before the interview, and ask them during the interview when you get the opportunity. Again, it shows that you've done some preparation and are serious about the opportunity.

When you're talking about your experiences in response to questions, try to show some enthusiasm / excitement about what you did. It's good to see that people are passionate about their work. Also, be honest about what your individual contribution was and what could've gone better. A decent interviewer will be able to tell anyway, so it's best to be up front about it.

All of this will help you to come across as a sociable, proactive person who's going to be a positive addition to a team.

## Prepare Good Examples

There are only so many things you are likely to be asked about during an interview for a job in software engineering. Therefore there's some useful preparation you can do to make sure you have some good examples to refer back to. Questions answered with real life examples are always better than answers based on theory. Having some of these prepared and to hand could be really valuable.

Using the [STAR framework](https://nationalcareers.service.gov.uk/careers-advice/interview-advice/the-star-method) (Situation, Task, Action, Result) helps to frame the story, so keep this in mind when you're preparing. It also helps to keep the story focussed and not go off on tangents (which is something I still struggle with and continue to work on).

A great example here would be a question along the lines of "Tell me about a time when you've had to manage stakeholder expectations". Most of us have probably been in a situation where we've been asked for the [moon on a stick](https://dictionary.cambridge.org/dictionary/english/moon-on-a-stick) and they need it next week. Talk about that project and the client, what they were asking for, how you handled it, and what ended up actually happening.

![The Tech Test](/assets/images/computer-screen-with-code.avif)

## The Tech Test

This is a controversial topic, and I see a lot of negativity around tech tests on LinkedIn. But here's the thing: tech is not a regulated profession like medicine, law or architecture. Pretty much anyone can have a go, and if you're good enough at it then you'll do well, and that's one of the many things I love about this crazy industry. However, what that does mean is that we don't have degrees and professional bodies to verify that people can do the job, so checking that someone has the skills they claim to have is down to the employer. Or put more concisely: "if I'm going to hire a juggler, I need to see them juggle".

However, not all tech tests are created equal. For me, it should be:

* Representative of what you'll actually be doing. If someone submitted a pull request where they'd implemented their own binary sort algorithm, I'd reject it straight away. So checking people can do something incredibly low-level isn't of any use, and puts off good people who'd be able to add a lot of value.

* Achievable in a relatively short time frame. For me, that means a 30 - 60 minute exercise. I've dropped out of a hiring process before because I've been given a coding exercise that would take weeks to prepare for. I simply don't have the time to do that, and it's unfair to expect other people to. 

* Collaborative. I always do my tech tests as a pairing exercise. It's more for learning someone's problem solving capability and their ability to work in a collaborative fashion, than checking whether someone has memorised all the core libraries of dotnet by rote.

* Inclusive. This is an area that I'm still learning about, but I am aware that different people have different requirements and it's important to take that into account when you're assessing someone's capability to ensure you're not ruling anyone out unfairly.

## System Design

This is quite a common element in senior interviews, and what I'm looking to assess here is someone's understanding of a system, how they consider trade offs and how they respond to being challenged.

As always, you can prepare for this element of the interview. Think about projects you've worked on recently where you have a good understanding of the technical architecture. The key thing here is to understand the product / problem being solved, but the majority of what you talk about should be the technical architecture. So have an understanding of the various components in the solution, how they were hosted, how they interact etc.

Particularly at a senior level, what I'm looking for here is the ability to describe trade offs, and get into the detail of the "why" as well as the "what". So for example, if you're hosting an API, was it serverless, was it in Kubernetes, or something else? And why was that decision taken? Similarly with data stores, did you use a relational datanase or a NoSQL solution, and again, why did you choose that option? 

I'll usually ask about what would happen if a sudden traffic spike hit the system, or there was a data centre level outage. If the answer to that is "there'd be downtime, because we didn't feel that the impact of such an outage would justify the cost involved in making the solution more resilient and scalable", then that's absolutely fine. It's just important for me to know that these things were considered.

Finally, I like to hear about what you learned in the process and what you'd do differently next time. I don't think I've ever worked on a project that I haven't looked back on and thought "Ah I should've done it this way instead". Being able to reflect and constantly improve is important.

## Development Process

I often think about an engineering function as a machine that takes ideas as it's raw materials and produces working software as it's output. Writing the code is only one small part of the process that the machine executes. My expectations will vary depending on the level of the role, but at all levels I'd expect some understanding of how this works end-to-end. It'll mostly break down into three high level phases:

### Planning

How does work get prepared? Does the team have a Product Owner who is responsible for maintaining the roadmap? At what point do the other team members get involved? How do you then estimate / prioritise the work? Is there a "Definition of Ready", and how well is that adhered to?

### Execution

Do you do a daily stand up, and what format does it take? What is your team's approach to collaborative working (pairing, mobbing)? What branching strategy does your team use? How does the code review process work? What continuous integration / delivery in is place? How do you know when it's "done"?

### Continuous Improvement

I love hearing about how people do retrospectives, as they vary so much and there's no right answer. The main thing I do believe applies universally is that there should be actions and owners as an output of the meeting. Prepare an example or two on of actual process improvements that the team have identified, what the team did about it and what the results were.

## In Summary

To re-iterate my earlier point, all of this is just my opinion and what I tend to be looking for as a hiring manager. Other hiring managers will disagree with some of my points, and that's entirely fair enough. However, there are definitely steps you can take to give you the best chance of success in that interview, and I hope the above helps someone land their next role.