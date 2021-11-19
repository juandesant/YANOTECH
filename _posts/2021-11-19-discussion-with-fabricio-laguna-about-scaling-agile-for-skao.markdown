---
layout:     post
author:     Juande Santander-Vela
title:     "Chat with Fabrício Laguna about scaling agile for SKAO"
categories: software, development, methodologies, agile, SAFe, large-scale infrastructures
---

I had a very nice chat with [Fabrício Laguna][1], The Brazilian Business Analyst, about how scale practices are helping us deliver the software for the SKA telescopes.

He also is the main person behind [Gigante Consultoria][2], which has the motto *"Assuntos Complexos com Leveza e Simplicidade"* (Complex Issues with Lightness and Simplicity), which I think is a great approach.

You can find the Video for that [chat in YouTube][5] (in English, with Portuguese subtitles, although automatic closed captioning is availabe), and I have embedded it below for your convenience.

<iframe width="560" height="315" src="https://www.youtube.com/embed/5omYrFtORLg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

And if you prefer, you can read the trascript of that conversation after the line!

Hope you enjoy it as much as I did!

<hr/>

[Music]

**Fabrício:** Hello and welcome to The Brazilian BA.

I have a guest today who is Juande Santander-Vela.

He's going to talk with us about the SKAO project. I'm sorry if i'm not pronouncing very well, Juande, but thank you for being here.

**Juande:** No, thank you for inviting us. It's a pleasure to represent the Observatory.
I think this is going to be fun.

**Fabrício:** Yes, I do.

I do have a question for you. I will give you some time to explain what the SKA Observatory project is, but the question I have for you is: «How are Agile teams working to create the world's greatest radio telescope?» 

**Juande:** Well, it's not a straightforward question to answer let's see if in some minutes we can explain it.

We are trying to build what will be the largest radio telescope in the world, and we're not creating just one, we're creating two of them, and we want them to operate as a single observatory: that's the SKA Observatory.

This means that we need to create one observatory for high frequencies in South Africa, and one observatory for lower frequencies in Western Australia.

We need to make sure that the environment is completely radio interference free, and we need to be checking when that is not the case so that we can remove the data when the data gets corrupted.

We are doing this with a partnership that includes countries from Canada to New Zealand, and almost every country in between, so we essentially operating from -9 UTC to +13 UTC, that is, we span 21 world time zones.

That means that we need to have a good framework, and a good way of creating working software.

The reason why we choose agile was because one of the main things when you have such a distributed workforce is that people need to be able to choose by themselves what's the most important thing that they need to do next. We cannot wait for them to wait to have a big planning session, and then tell them this is what you do, and this is what you do, and this is what you do to every single team… and then when there are problems you need to come back again and tell them individually okay, you solve this problem this way, you solve this other problem this other way, you solve that other problem this way… This doesn't work.

There is no way that this approach can work, because for the amount of people that we need, which is in the order of 200 people, that means that you can have in the order of 40000 interactions, because those are all the connections that those many people can have together.

So what we are doing instead is trying to first have a way to organize the teams, doing it in a way that delivers the best result. 

And we were looking into agile practices because we wanted the customer…

Well, in this case the customer for a radio telescope is a little bit more difficult to define that for…

Frabricio:

Um, the customer it's not an alien, is it?

**Juande:** No, no, no, the aliens are not our customers [Laughter]

We have two kinds of _customers_: while we are developing the telescope, the customer is essentially the astronomers that will validate that we've built the right thing. But when we reach the operations phase for the telescope, the customer will be the astronomers that want to do interesting things with our radio telescopes.

So we are now focusing on our first kind of customer, because the other kind of customer will only come later, when there is a facility for them.

In the end, trying to find different methodologies we chose SAFe, the Scaled Agile Framework, because it was very well known across all of the world so you could have people certified in any of the countries that work for the SKA project. So that was a big plus for us. 

We actually did a kind of an auditioning for the different frameworks, and Ian Spence from Ivar Jakobson was the person that really clicked in the way we were thinking together.

So we started training people in SAFe, and we now have what we call three Agile Release Trains combined into a SAFe Large Solution.

To make it all more complicated, we come from a very waterfall-oriented design phase, in which we had gates, and we had to pass a Preliminary Design Review, and then we had to pass a Critical Design Review, and then we did we did an aggregated System CDR... We also have what its called an Integrated Product Schedule (IPS).

If we were working in a normal way (for this kind of facilities), we would be following the IPS to the letter, and these would be the milestones, and this is what we're doing, and then it would be very difficult to introduce change, or adapt to change in these circumstances.

Using SAFe has already given us very many benefits.

Typically in this kind of project, when you have the this kind of IPS, it says "within three years you will receive x black box", and then you will try to interface with this black box, and there is no way you can change the black box because the process to create that black box already finished: there is no one there. There might be some maintenance, or there might be some support contract, but to change it meaningfully, that's something that you cannot do.

**Fabrício:** That's the idea of waterfall. Exactly, you finish in a stage and start a new stage.

**Juande:** Exactly, and there is a bit of merit to that when it's really difficult to change things. So, if you were building a machine, physical machinery which a lot of big parts that really need to be assembled together in a very careful way, and they need to be tested, and each test is ve***Fabrício:** *ry expensive, then you can only afford to do that once in a while.

With software, most of the software you can really iterate and test very quickly. 


**Fabrício:** I see, when you talk, the value of working with an approach that can accommodate change, that can embrace changes, opportunities, and how hard it will be if you had a traditional process for for doing that.

**Juande:** Yeah

**Fabrício:** With this huge amount of people in different countries working in the same project you would need to have a very detailed plan for people to to work on, but you are being able to accommodate change inside of that, that's wonderful.

**Juande:** But also part of the problem is that if you do a very intense plan where you also plan to utilize everyone that is contributing to that project at 100% of the time, any time you have someone that has a family issue, or has a health issue, or retires from the project, you get an impact of trying to get someone else, and get them on board.

So one of the things that we are also embracing is  that we have dedicated time for introspection, what went well in the last three months, and what didn't go so well, what we could do to to improve things. We have several people in what's called in SAFe the Lean-Agile Center of Excellence, which is a bit of a grandiose name for it, but essentially is a number of people that have gone through the SAFe Program Consultant training, and we try to influence how the organization works, and trying to make them see the benefits of not having everyone running at 100%, and the innovation that you can get when you can get some some of these people with some free time.

But it is also very important to have this alignment: you tell them what you want to do, but you don't tell them exactly how you want them to do it, and that's why they can come up with different approaches. Again, if you go the very detailed plan, the client says you must do as I say, and this is the design that we have, and you have to follow it. But these teams they said: well, we need to get this data, we need to produce this other kind of data, this is what the astronomers are interested about... what if we change this box in the middle and we can use something else instead? And

That means you need to be also very open about what you need, and what your potential issues are, and sometimes we cannot tell them exactly what we want, because it needs to be tested, and this is also a level of openness that in other projects... telling a provider that you don't know something, is kind of... 

**Fabrício:** A weakness?

**Juande:** That might be exploited by that provider. So the other thing that we're doing is that we embracing something called relational contracting,  which is the theory that if you have contracts that instead of being transactional --- this is what I
get, this is and this is what you get, and that's all --- you try to build a  relationship with your providers, and you can increase your your mutual transparency. Then that benefits everyone, because they can get more opportunities from the knowledge that is inside of their organization, and you can get better service because they can understand better what you need.

And if you tell them that something is not going as well as you expected, they can adapt to that more quickly.

And they also have the idea that this is for the long run of the whole of the project, so not everything needs to be nickeled and dimed, trying to say well, this cost me two more cents that it used to,  or this is making me work two more hours...

**Fabrício:** I like to call it the difference between contracting outputs and outcomes.

When you have a very detailed plan, you are contracting outputs, and so your providers have to deliver you exactly what you said in the outputs you have to deliver to you, and when you contract for outcomes, they start to be accountable for the outcomes, and they have to decide what are the necessary outputs to bring that outcome. They have to think 
about the steps, they have to think about the solution. You're not expecting a specific solution, you are expecting a specific result, or any specific outcome, and that relationship requires a lot of trust, otherwise it would not work.

**Juande:** Exactly, exactly.

**Fabrício:** If people want to share information with you, people who are running big projects, and I say very big projects, and want you to use Agile or SAFe on it, how can they reach you?

**Juande:** Well they can [find me on LinkedIn][3]:, that's one way. 


I'm also on twitter, [@juandesant][4], and if you go to the SKAO website you will also find my email there.

Please, feel free to reach out, we just love to have this project, and to have more people contributing to it.

**Fabrício:** 
I will add those addresses below this video. If someone wants to to check on and to know more about the SKA Observatory, it will be very interesting.

Thank you, Juande, and thank you everyone who is watching us.

**Juande:** Thank you, Fabrício, it's been a real pleasure

[Music]

[1]: https://twitter.com/fabricio_laguna "Twitter: Fabrício Laguna (@fabricio_laguna)"
[2]: https://giganteconsultoria.com.br/ "Gigante Consultoría: Educação Corporativa"
[3]: https://www.linkedin.com/in/juandesant/ "LinkedIn: Juande Santander-Vela"
[4]: https://twitter.com/juandesant "Twitter: Dr. Juande Santander-Vela (@juandesant)"
[5]: https://www.youtube.com/watch?v=5omYrFtORLg "YouTube: Como equipes ágeis estão trabalhando para criar o maior radiotelescópio do mundo? (English, Portuguese subtitles)"