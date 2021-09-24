## #1 Checkpoint: Of Debugging & Deadlines

I completed my probation at [Unacademy](https://unacademy.com/) - developing (more like debugging) the frontend for live classes. It is a small-time but feels like a long time. They weren't lying when they said work at a startup is fast-paced - not to mention the exponential learning curve. I worked in a rapidly growing team, learned new technologies, followed best practices, solved 100s of bugs, shipped 2 features, and faced production bugs & rollback. 

I wasn't sure that I will make it through probation. The memory of my first days is still vivid.  I was going from person to person - looking for advice to put my best foot forward. Good folks from the community helped. I picked up some handy tips but as they say - you learn the most by doing. To be honest - not a lot has changed. I am still struggling. But I do see a path shaping up. And with the benefit of hindsight - a few learnings. 

So, here are my two cents. Best served to folks starting on a new job - unsure of themselves.


# Communication

It's the old cliche that communication is really important. You have probably heard it before. But it bears repeating - even more so in the remote setup. 

**High Agency**: It is your job as the newbie to reach out. To ask. To question things. In good places - nobody is going to mind a good question. But you must try to figure out things on your own as well. Sometimes, I reached out to a senior too early. In a fast-paced remote environment - you need to respect senior folks' time. 

For most cases - spend an hour or two (with a break or more in between) with the problem before reaching out. Keep your queries concise and to the point. Tell all the things you have tried.

It's a tough balance to master - when to ask & when to figure out on your own. I am still struggling to hit the right balance. But in the start - you can err on the side of asking.

**Estimates**: Be honest with yourself and your teammates. If you don't know something - be very clear about it. If you need more time to do a task - be very clear about it. You are new and unfamiliar. What takes 10 min to achieve for your senior may take an hour or even the whole day for you to accomplish. It's okay.

 I have struggled with this. When a senior gives an estimate - it's hard to put a counterpoint but having that awkward conversation helps you avoid drudgery afterward. And again - it's okay if your estimate is wrong. There are always edge cases. You can never have a perfect plan. 

**Document**: Document your learnings. The patterns followed at your place. The common errors. The bugs you solved. This has two-fold benefits. You learn from your mistakes. You help the future joiners.

**Explore**: Reach out to folks from different teams. Participate in events going on in the company. This gives a better insight into the company and prevents you from getting pigeonholed to your team.

# Ownership

I could have put it in communication only but I think it is worth having it as a separate heading. This is one quality that I have found to be the most desired by the seniors.

You are given a task. You get it done. Period. If there is any blocker - you figure out a way to remove it. It is your responsibility. The earlier you start taking ownership - the better your odds at your job. 

# Health

Take care of your health. 

You cannot operate from a place of fear - fear of not performing well, of getting laid off. One must embrace uncertainty. Have an abundance mentality. Given enough time - you can master anything. 

**Patience and grit.** 

Many times I gave up too early on a bug and reached out for help. I am trying to decrease this. There are lessons to be learned while struggling with the bug. Don't take the easy way out. In the short run - problem will be solved but this will harm you in the long run. Having said that - don't do the opposite either. Reach out to your peers. You learn a lot when you pair-program. The ego has no place if you want to learn.

**Sleep, take breaks, drink water, and stretch.** This is the best debugging technique. Far better than the ones I am going to mention below.

I neglected my health in the last few months. I remember the marked difference it made when I had slept properly vs when I had not to the kind of code I wrote. 

# Technical Skills

While the general principles hold true for any discipline - this section will be more relevant to a frontend developer.

Unless it's an early age startup - you are likely to encounter a huge and complex codebase. If it's a startup - not all the best practices would be followed. There will be technical debt. No extensive documentation. You get the idea. It can get intimidating real fast. You need to make your way through it slowly. Understanding the different pieces and refactoring wherever you can.

**The flow**: At the start, you will probably be restricted to a small part of the codebase. You must do your very best to understand the flow of things in that particular part. A senior will probably guide you - question and cross-question every little thing. Tinker with the code yourself to figure out how things are working. **Check the data. Put logs everywhere.** I got lazy in this step and paid dearly for it afterward in long debugging sessions.

**Chrome DevTools** is your best friend. Spend some time learning the different tools at your disposal. It will help you a lot. Start with this [video](https://youtu.be/TcTSqhpm80Y).

Level up your** CSS **skills. As a new joined - you will probably be given UI-related tasks. Check out this [article](https://engineering.kablamo.com.au/posts/2021/my-first-css) for main CSS concepts you should know. I am currently learning CSS following this [course](https://web.dev/learn/css/) by Google.

Make sure you have a good understanding of the main [**JS** concepts](https://www.freecodecamp.org/news/javascript-interview-prep-cheatsheet/), especially, the trickier parts like closures and event loop. If you don't understand them - you will have a hard time figuring out bugs. For starters - you can watch [Namaste JS](https://www.youtube.com/playlist?list=PLlasXeu85E9cQ32gLCvAvr9vNaUccPVNP) by Akshay Saini.

If you are working with **React**. Get comfortable with both class components and functional components. Don't just learn hooks. Learn lifecycle methods as well. You will find a lot of code written in the old style. Also, both approaches have different advantages. Understand the tradeoffs.  Very important - understand [how the state gets updated](https://dmitripavlutin.com/how-react-updates-state/). You might think you know it but there are nuances. Same for [Redux](https://redux.js.org/tutorials/fundamentals/part-1-overview). 

Good resources for the same - official [docs](https://reactjs.org/docs/getting-started.html) and [blog](https://dmitripavlutin.com/) by Dmitri Pavlutin.

Learn **Backend**: Well - not completely but have a basic idea of how things are working on the backend. This will actually improve your understanding of the front end. It should not be a black box to you. In the same way - learn design and product as well.

I was working with Web Sockets on the front end.  Learning just the basics of the implementation on the backend helped me understand the flow of things better. I am currently learning more from [Hussain Nasser](https://www.youtube.com/c/HusseinNasser-software-engineering). Highly recommended channel.

**Checklist**: Things which you need to do on a repeated basis, like adding a JIRA/Linear ticket to a PR. Make a checklist for them. This will help you avoid silly errors. 

You can also log the idiosyncrasies of your codebase in your checklist. The different scenarios you need to take care of. For example, in my team, we have to write code according to roles - whether the user is an educator or a learner. We maintain a global flag for the same.

And that brings us to the end of this article. I have by no means become a master at my work but I do feel a little more confident about myself. I can see visible improvement. The journey is long and I am learning to enjoy it. If you made it this far - I hope my ramblings were of some use to you. I would love to hear your experience/feedback.

Also, check my [newsletter](https://buttondown.email/rajatetc/) where I share useful resources to get better at development among other things.  









