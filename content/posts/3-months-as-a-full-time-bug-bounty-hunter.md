---
title: "My First 3 Months as a Full-Time Bug Bounty Hunter: A Journey of Highs and Lows"
date: 2025-10-08T00:00:00-03:00
draft: false
cover:
    image: "/img/3-months-as-a-full-time-bug-bounty-hunter/cover.jpg"
    alt: "3 Months as a Full-Time Bug Bounty Hunter"
    caption: "3 Months as a Full-Time Bug Bounty Hunter"
---

A few months ago, I made a huge decision that changed everything: I became a full-time bug bounty hunter. Three months later, I can't help but feel this may have been one of the best decisions I've ever made in my career. I feel compelled to share my thoughts and mindset here for two reasons: first, to keep this blog active, and second, to help and motivate others.

The hardest part of writing this post is finding the right balance between what I feel safe sharing and what I believe will be valuable to my readers (see the Venn diagram below). If there's anything you'd like to know more about, have any questions, or feel I've missed something, please send me a message.

![Venn diagram of things I feel safe sharing versus things I believe people will find valuable](/img/venn.png)


## From Building to Breaking

If you've read my [latest blog posts](https://vitorfalcao.com), you'll see that I am highly technical. I have a degree in Software Engineering and worked as a developer and SRE for years before realizing I was on the wrong path. I was pretending to be happy instead of accepting the challenge of taking a step back to restart my career in cybersecurity, an area I truly love. However, I have no regrets. The developer experience gave me a deep understanding of the inner workings of the applications and products I now hack. This knowledge is indispensable and has improved my hacking mindset.

It's important to say that I don't believe your background defines you. The bug bounty community is filled with people from all kinds of backgrounds, and I believe this diversity is our superpower. For example, there's a [crazy cardiologist](https://x.com/xssdoctor) who can hack any target in minutes!

So, whatever your background is, believe me when I say that you have a unique perspective that can help you find bugs no one else would. Don't give up, because the first step to becoming good at something is being bad at it.

## Month Zero: Preparation for Full-Time Bug Bounty Hunting

I believe being ready and prepared for as many outcomes as possible is the best you can do. For example, if you want to go full-time bug bounty, make sure you have enough savings in case it goes wrong. Also, if you haven't read [Critical Thinking: A Full-Time Bug Bounty Blueprint](https://www.criticalthinkingpodcast.io/p/how-to-go-full-time-bug-bounty/), that's a great place to start.

For me, one of the most important prerequisites is ensuring you have a decent financial cushion. I had enough savings to last for months in case I didn't make a single penny from hunting, so I shouldn't have felt pressured or anxious when I started, right? Well, I did anyway.

It turns out our minds are complex machines with infinite variables that are impossible to predict. I can't recommend therapy and cultivating a growth mindset enough. You don't have to have complete control over yourself, but you do need to understand and accept your mindset. To be honest, that's not easy.

Although I won't dive deeply into these preparations, as that could be a blog post in itself, there are other challenges to consider. For example, is your home office ergonomic? Can you remain productive without a manager setting deadlines? Do you have a plan to maintain an active social life without the daily interactions of a company office?

I hope those questions provide some food for thought. Now, let's move on to the hacking part.

## Month One: Triaged Reports, Zero Payouts

I started by targeting Google Cloud, and I was very excited because [rhynorater](https://x.com/rhynorater?lang=en) (Justin) has pumped me up telling me I'd do great. However, you may know how hardened Google may be, and it was not an easy journey. The more time you spend without finding anything, the harder it becomes to find something. At some point I took control of this (not easy) and started finding bugs. Google VRP pays very well, so this was a major reason I chose them, one bug could be enough for the whole month.

By the end of my second week, I had a few Google Cloud reports in the pipeline awaiting that "Nice catch! 🎉" notification. I then decided to look at another public program on HackerOne, partly because they sponsored the Critical Thinking podcast, and I'm a big supporter of their work. That went incredibly well! I submitted several reports, expected some good bounties, and started to feel like I could hack anything. It was the snowball effect I needed to build my confidence.

However, I ended the first month with no bounties paid out. This is a common challenge for any full-time bug bounty hunter: a "triaged" status doesn't guarantee a payout. Even when a bug is confirmed, you often don't know the exact amount or the payment date. I believe this is why working with programs you trust and have experience with is so valuable. Although I had planned for this delay, handling the uncertainty still wasn't easy.

![Google VRP Award: Crickets: Wait a month for the VRP panel decision](/img/crickets.png)


## Month Two: Bounties Started Rolling In

It turned out that two of the Google reports I had submitted weren't going to be paid. The VRP panel decided that while the issues would be fixed, they didn't meet the criteria for a financial award. A primary reason for this was that I didn't fully understand the specifics of how Google's Cloud VRP works. Again, this was a possibility I had planned for, but that didn't make it any easier to handle.

Then, the bounties from the HackerOne program started coming in. It's hard to put into words what it felt like to receive my first bounties as a full-time hunter. The best part was that this single program paid out what amounted to three times my monthly goal. To top it off, while I was in Miami waiting for a connecting flight to DEF CON, I received another "Nice catch! 🎉" and a reward message as I stood in the customs line. I almost hugged the random guy behind me. It’s the typical bug bounty roller coaster of ups and downs that we love.

At the end of the second month, I was on a fantastic motorhome trip around Banff, Canada, with my partner and a few friends. It's an amazing place, and it was great to be there while still seeing bounties hit the bank account. Then, I received an email inviting me to my first-ever Live Hacking Event: Google BugSwat Mexico.

![Banff](/img/banff.png)

## Month Three: The Google BugSwat

Getting invited to an LHE was one of my main goals, and I thought it would take at least a year to achieve. However, rhynorater nominated me, and I was accepted. I am very grateful to both of them for believing in me. So, it was time to get ready and hack Google.

I had no previous experience with LHEs, so I decided to do some light hacking on Google. Main objective was to gather target-specific knowledge, while also spending most of my time resting to avoid burnout so I could be at 100% for the event. I also made preparations to ensure I could be fully focused during the two-week event, like talking to my partner about it, adjusting my routine, and clearing my schedule.

Although it may seem like it was an easy ride, I had to battle impostor syndrome and frustration during my preparation. I've recently realized that I'm not alone in this and that most top hunters also struggle with it. Discussing it with some people helped a great deal.

A few days before the event, [monke](https://x.com/monkehack) (Ciarán) sent me a message asking if we could collaborate, since none of his teammates were going to participate. Knowing him from the CTBB community, I didn't have to think twice, and I accepted immediately. We discussed our weaknesses and strengths, the bounty split, etc., and we were ready to go.

The event kicks off, we receive the scope, and we begin hacking. I decided to focus on what I do best while targeting the highest-paying assets. Throughout the event, monke provided a lot of guidance on how to manage my time, avoid rabbit holes, and maximize the bounties. Soon, I started finding bugs and the dopamine kicked in. Then, monke started finding good leads, and we began writing reports.

By the third or forth day, we noticed we were submitting one or two bugs per day, so we set a goal to report at least two daily until the end of the event. However, knowing this pace could quickly become unhealthy, we made sure to take breaks and cover for each other in the meantime, like when I took time off for my birthday. Whenever one of us took a break, the other would "lock in" to keep the momentum going. Also, even when one of us was away, it was fun to voice our thoughts and brainstorm on Discord. We had some great laughs about our "stupid" bug ideas that ended up being accepted.

![My reaction after monke told me about one of his stupid ideas](/img/discord.png)

We arrived in Mexico and had great days of on-site hacking. We met and collaborated with [Adnan](https://adnanthekhan.com/), ate amazing food, and chatted with the Googlers, who are all spectacular people. Overall, we had a lot of fun. We even managed to submit a few bug reports just ten minutes before the deadline. I also can't forget how badly jet lag affected me for days, so I had to drink a massive amount of coffee.

Then came the last day of the event, when the winners were announced. I spoke with monke about it, and we decided not to set our expectations too high because we were competing against some truly amazing hackers.

Later, at the wrap-up party, they started announcing the winners. When they were about to name the Best AI VRP Researcher(s), they mentioned a pair that had managed to submit 14 valid AI reports, and that was me and monke! We won the award! What impresses me the most is that we didn't have a single duplicate, that's insane!

I was already quite happy when they began to announce the second-place overall winner, mentioning the 14 valid reports again. As it turned out, we had won second place as well! I was so happy to receive two awards at my very first LHE, which just goes to show what a roller coaster bug bounty is. It's full of ups and downs, but the thrill makes you want to get back on and do it all over again, no matter what.

![Monke and I winning the 2nd place award](/img/award.png)

## We Keep Riding

To wrap things up, my first three months have been a true roller coaster, but the freedom and learning that come with working as a full-time bug bounty hunter are incredible. This journey is just beginning, and I plan to share more of the highs and lows along the way.

If you want to follow my progress and get more bug bounty insights, the best way is to [follow me on X (Twitter)](https://x.com/busf4ctor). Let's keep riding.