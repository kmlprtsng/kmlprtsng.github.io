---
layout: post
title: Choosing a hosting for NopCommerce – My Experience
---

**Short Story**

I had a lot of trouble with one of the recommended NopCommerce hosting provider and so later on went with Everleap (which is also recommended) and I’m much happy now.

I’d recommend going with [Everleap](http://www.everleap.com/a/rflhxs) or at-least try out their trial version before choosing your hosting provider. They offer 30 day free trial so you won’t be wasting any money if you don’t like it.

Also no matter which hosting provider you are with, run your website in 32 bit mode as the memory usage is much less. Everleap by default runs the sites in 32 bit mode. 32 bit websites use less memory than 64 bit sites. Period.

You can look at the site [www.firstworldRx.com](www.firstworldRx.com) which is running on [Everleap](http://www.everleap.com/a/rflhxs) here.

**Long Story**

OK. So the scene was set. One of my clients asked me to make an eCommerce website for them and having my strengths in ASP.NET and C#, I was looking for something well written in these languages so that I could easily extend them as some hefty changes were required. So low and behold I went for [NopCommerce](http://www.nopcommerce.com/). I was pretty happy with it on my local machine as it is a fully fledged eCommerce system that you basically get for free but then came the big decision. Hosting……

So I looked around and went with one of the well known web hosting provider. I don’t want to mention any names here but they were one of the recommended one by NopCommerce.

> So let the journey of pain begin

So here I was thinking that I’ve got a brand new hosting provider, recommended by the people who made the software and what could possibly go wrong. And boy did something go wrong.

The performance of the site was shambolic. The website took 60 seconds to compile and show the page when it loaded for the first time. That is 60 seconds. Give or take 5 seconds. Can you imagine serving site to a customer at that speed. But that only happens if it’s the very first time the website has loaded or the app pool has recycled.

So thinking that if the app pool recycles only once a day then we can live what that. It would be really unlucky for a customer if they were to come to a page at the exact time when the app pool recycled. NopCommerce has a a schedule task that keeps the website alive or brings it to life if the app pool recycles.

> Shock horror!! Boom!!

Well, the application pool recycled not every 24 hours but every 5 minutes or so specially when there was some sizeable activity on the site. Now come on, does anyone expect that from any site. It was like being put on a deserted island all by yourself with tigers and lions. Making it out alive out of the island looked like a mirage.

> Leave no post unturned.

So, my conquest began to increase the performance of the site. By this time I am starting to blame NopCommerce for being slow like a dying snail. Have a search on google and you will see what I mean as there are few forum posts from people complaining about the same thing.

Then I look under the hood and guess what. I see 1.2 GB of ram being used when the website is in the idle state. 1.2 GB and I’m not kidding. I was enraged. Come on what kind of site uses that much memory with hardly no customers at all. And when there were a few customers I suspect that pushed the memory limits and caused the site to recycle it’s app pool because how much weight can an ill horse really take. I really needed an elephant so I pleaded to the hosting provider to give me 2GB of ram minimum. But they weren’t playing the ball.

So I dug deeper and deeper and found the cause to be the app pool running in 64 bit which has it’s benefits. So once again I went back to the hosting provider, asking them to get the app pool to run in 32 bit and the whole hell went loose. The site broke but I like a lover with a broken heart just wanted it to work in 32 bit mode because I knew the other route was like dying the death of boiling lobster. The website threw a complier error. I persisted and after about 5 minutes the first page came alive as if the dead patient has just been revived. Then I went to the next page and kept reloading until it worked and then the next and then the next. This was slow and painful however the site was now using about 300MB in the idle state so I was happy.

> You can only drag a dead horse so far

So the site was now not giving any complier error but deep down I knew that if I was to do another update to the site, it could all go pear shaped again and my most scary nightmares came true. I deployed my latest changes to the hosting provider and the same thing happened again. This time I asked my hosting provider to fix it once and for all but they just couldn’t do it. They kept flicking between 32 and 64 bit and I was only to wise to pick up their trick when they kept innocently changing it back to 64 bit. The truth is that they could not support 32 bit websites. There must have been some configuration issue with their server because I could load the same files downloaded from the server on my locally hosted IIS and they all worked fine. So it can’t be the corrupt dll etc.

> Take no prisoners

Finally, either by luck or destiny, we had to leave the web hosting company and at that time I was pretty much ready to leave so now came the time to find a new partner that could serve our needs. Everleap looked like just that partner but I had my doubts but I decided to take the plunge with the free 30 day trial. By day two I was impressed and asked my client to purchase the everleap hosting and by day three, the hosting of the site had moved to Everleap.

> When you are in love then the whole world is your friend

Everleap runs it’s site in 32 bit mode so it was using significantly less memory than my previous hosting provider. In it idle state it is consuming around 271MB and in the last 3 days, the app pool hasn’t even recycled once. The initial page loading (including compiling time) is around 5 seconds and after that it is all a game of milliseconds. The site is being served by 2 cloud servers so there is that delicate play of load balancing. Overall, I am impressed by how performant the website is. No longer do I blame NopCommerce for being slow.

There were of course big considerations for us when deciding to go for Everleap such as the cost of the IP SSL which is $15 per month but we are happy with SNI SSL ($29 per year for RapidSSL), which is the way forward, specially with the sites in cloud which could span across many servers.

Once thing about Everleap though is that they don’t have live chat and for any support you have to raise a ticket which I didn’t really like at first. I have always been used to live chat when there are some problems. However, I must say that Everleap’s ticket system hasn’t caused me any major issues so far. Sometimes they are very quick and sometime I have been able to solve the problem myself before they have even replied to my ticket so that is something to be vary of but they are generally pretty quick at getting back.

**Conclusion**

If you are in the same boat as me and are debating whether NopCommerce is a viable option for you because of it’s performance then definitely give Everleap’s 30 day trial a go and then choose for yourself what you want to do. As far as I am concerned, [Everleap](http://www.everleap.com/a/rflhxs) Rocks!!