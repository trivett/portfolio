---
layout: post
title: Ignorance is nothing for a programmer to be ashamed of
date: 2017-03-01 19:44:15.000000000 -05:00
type: post
published: true
status: publish
categories:
- Blog
tags:
- career
- web development
- technical interviews

excerpt: "Make a production-like development environment in a few minutes."
---
In the past week, some really prominent programmers made an incredible thread on Twitter that basically shattered traditional tech interviews. It started with the creator of Ruby on Rails, race car driver, prolific blogger, and all around opinionated genius, DHH.

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Hello, my name is David. I would fail to write bubble sort on a whiteboard. I look code up on the internet all the time. I don't do riddles.</p>— DHH (@dhh) <a href="https://twitter.com/dhh/status/834146806594433025">February 21, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>


He's referring to [a crude and inefficient algorithm for sorting](http://www.algorithmist.com/index.php/Bubble_sort) (which is excellently visualized through [Hungarian folk dance](https://www.youtube.com/watch?v=lyZQPjUT5B4) and the common technical interview scenario where a young programmer is asked to create an implementation of a sorting algorithm, on a whiteboard while his interviewer watches on.

The thread had quite a few gems to it like this one:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Hi, my name is Nate. I&#39;ve been coding JavaScript for years and I still have to Google how to send ajax requests. <a href="https://t.co/ovyrsDq7jZ">https://t.co/ovyrsDq7jZ</a></p>&mdash; Nate Higgins (@nathggns) <a href="https://twitter.com/nathggns/status/835669591691051010">February 26, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

So relatable. I often find myself feeling like a dope for googling something simple like the length of a Python string, or doing something really beginner-level wrong. Like for instance, I often make the mistake of treating Ruby hashes like JavaScript objects, and try to get values out of them with dot notation. That's only derpy if you assume that everyone was put here on this shitty planet with a perfectly functioning Ruby interpreter in their heads.

In _Infinite Jest_, which I am currently halfway through and thoroughly recommend, David Foster Wallace has one character, an agent for the "Bureau of Unspecified Services" admit that "technical interview" is agency jargon for torture. The coincidence is apropos. I admit that I really really suck at this. I've had my share, but thankfully never had to actually write code on a whiteboard, but mine were all uniformly atrocious. Imagine the situation. You are in front of some people who will make a decision that will affect you for years. They hold your career in their hands. And to safeguard your livelihood, you have to write out code or pseudocode in front of them, in real time, without any of your familiar tools. What a great way to assess someone's competence!

If that isn't stressful enough, try taking a 24-hour flight, then getting the same insane exercise from rasicst punk customs agents threatening to deport you. This literally happened to [Andela developer Celestine Omin](http://www.recode.net/2017/2/28/14764064/nigerian-software-engineer-detained-by-us-customs) just this week.

Algorithm memorization and brain teaser-like puzzles do not reflect well at all on someone's ability to code and solve problems on the job. For instance, if I needed to sort an array, why on earth wouldn't I just use the native implementation for sorting an array in my language of choice? I can spend a lifetime thinking of my own sorting algorithm, and it won't come close to Ruby's [Enumerable#sort](https://ruby-doc.org/core-2.1.0/Enumerable.html#method-i-sort) in terms of efficiency.

Seriously, if you are at work and you see someone writing their own version of `.sort`, you have a time waster on your hands.

Since I mentor alumni/ae of General Assembly's Web Develpment Immersive, I see this all over the place. Students come in for help with these inane interview questions, or even a [whole book](http://www.barnesandnoble.com/w/cracking-the-coding-interview-gayle-laakmann-mcdowell/1122334602) on just getting through these torture like interviews, when they should be nailing down the basics of JavaScript and getting practice by solving actual problems. Making their own applications, building things. That's what you do on the actual job.

Furthermore, I think that forcing someone to code without documentation, or use of the internet is completely against the whole schick of programming that drew me to it in the first place. This is the only industry that I have ever worked in that totally accepts a level of ignorance.

There's a scene in _All the President's Men_ where Bob Woodward asks who someone is, and his editor says he oughta just send him packing right now. How can you, a journalist, not know the name of so-and-so cabinet secretary.

That makes sense for a journalist. That name might be on a manifest for some shady shipment or something and if you don't recognize the connection between that and high levels of government, you aren't doing your job.

But programming is different. There are so many languages and frameworks, and even if you just specialize in one, there is no way you can be expected to know every little thing about it. This is why we have documentation and Stack Overflow.

Back when I was just noodling around with web development and I straight up had no idea what I was doing, I did a [fun hackathon](www.publishinghackathon.com/) with a more experienced developer. I didn't think of myself as a 'real' programmer at the time. I was just starting out. I did what I could for the [app](http://www.bookciti.es), but practically none of it was my code.

One thing that stuck with me, was noticing that around the room, all of the 'real' programmers were mostly looking at Stack Overflow the whole time, looking for ways to solve whatever problem they are on at the time. You only see a terminal or a text editor on the screen half the time.

That might sound like nothing really, but it helped encourage me to keep learning. I loved that you don't have to know everything to just get started. Just learn one thing at a time while you make cool stuff.

At a Rails conference that I went to last year, I met a young developer, fresh out of a bootcamp who actually _gave a talk_ on something. That takes some chutzpah! I thanked her for the presentation and chatted a bit. Prior to bootcamp/web development, she was an English PhD student. At some point during the few minutes we chatted, I used some word that she didn't remember the meaning of and she just asked me what it meant. She remarked on how refreshing it is to just admit ignorance and not feel like you are being judged. If that came up in academia, she would have just pretended she knew what it meant and felt ashamed.

I think that interviews should reflect the actual job. Don't put people in the least comfortable position possible. It's way more helpful to see how they approach problems, how the seek help, how they test, how they use git, etc. For the small number of times I interviewed people for technical positions, I had them make a thing on their own time, with no time limit, but a strong suggestion that they don't go completely nuts with it. (I hate that this is essentially unpaid labor, but especially for a junior, I think it's nice to have that little extra practical experience.) That gives me an idea that they know at least some stuff, then we can take it from there. The next part of the interview was to pair on fixing something or adding a feature to the mini-application together.

There are problems inherent in this too. Not everyone gets away with admitting technical ignorance. It's easy for me, a white, college-educated dude in my early 30s to just blithely dismiss ignorance as just part of growing as a professional, but it's used as ammunition for the small population of dickheads in tech that just LOVE to put down women for not being 'real' engineers. Some of the 1337 haxors on that twitter thread said the same:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Hi. I&#39;m Estelle. I&#39;ve been developing websites since 1998. As a woman in tech I don&#39;t announce my code shortcomings for fear of consequences <a href="https://t.co/rEFKEO7ec7">https://t.co/rEFKEO7ec7</a></p>&mdash; Estelle (@estellevw) <a href="https://twitter.com/estellevw/status/836228371361091584">February 27, 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

I can see this happening. Older dev hasn't 100% grokked ES6 features by heart? Dinosaur. Female/POC dev asks for help on a tough feature? Amature. Bootcamp graduate learns something new on her first day on the job? Why did we hire this person?

Making people do free work that you don't need to prove that they can code is also problematic. What if you have kids to take care of? A demanding job? Two demanding jobs?

The way that we hire people is nuts either way. I wish I had a better idea to propose, but I just think that hiring managers should value applicants that are willing to admit that they don't know everything, but are willing and able to learn.
