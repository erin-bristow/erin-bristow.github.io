---
layout: post
title:	"DEFCON 30 - Recon Village CTF Writeup"
date:	2022-08-18 12:00:00 -0700
categories: OSINT CTF
---
After spending Friday of our first (!!) in-person DEFCON wandering around, on Saturday my friend [Jeffrey](https://github.com/j-hertzog) and I decided to plop down in the [Recon Village](https://www.reconvillage.org/index.html) and work on their CTF for a few hours. Team Trojan tied for 4th out of 59 teams.

**Note!** This is currently still in dev, will finalize it this weekend.

# Table of Contents
1. [DEFCON!](#defcon)
2. [Writeup Intro](#writeup-intro)
3. [Challenges](#challenges)
	- [Challenge 2 - Tax Fraud LTD.](#challenge2)
	- [Challenge 3 - Spammy email domain!](#challenge3)
	- [Challenge 4 - A person named Phonenumber](#challenge4)
	- [Challenge 5 - Pool Party, Pt. 1](#challenge5)
	- [Challenge 6 - Pool Party, Pt. 2](#challenge6)
	- [Challenge 7 - Callum, Pt. 1](#challenge7)
	- [Challenge 8 - Callum, Pt. 2](#challenge8)
	- [Challenge 11 - Eva Hesington](#challenge11)
	- [Challenge 16 - Find the volcano!](#challenge16)
4. [Conclusion](#conclusion)


## DEFCON! <a name="defcon"></a>

DEFCON was very very cool! Yada yada yada will probably throw some pics in here of badge and googly eye vandalism and such.

## Writeup Intro <a name="writeup-intro"></a>

Last year's challenges were more difficult. Many went unsolved, and Team Trojan secured 8th place with only three solves. This year, we solved nine challenges and tied for 4th! We had a great time competing, so a big thanks to the organizers of the CTF.

![Scoreboard](/assets/post3ctf/top5.PNG)
<p align="center"><em>Graph showing the progress of the Top 10 Teams</em></p>

The CTF began on Friday and we started on Saturday, so we had a bit of catching up to do (in the above graph, we're the purple line that started second-to-last)! 

![Challenges we solved and the time when each challenge was solved](/assets/post3ctf/challengesSolved.png)
<p align="center"><em>Our solved challenges with timestamps</em></p>

Notes:
1. This CTF included profiles and online information for real people. Therefore, some information has been redacted in this writeup.
2. The number of solves for each challenge is the number when we first solved that challenge. We did start late, so there weren't too many solves after us.

## Challenges <a name="challenges"></a>

### Challenge 2 - Tax Fraud LTD. <a name="challenge2"></a>
*100 points, ~45 solves*

**Challenge Description**: Cherry Software LTD is associated by address with a questionable business registered on August 4th. On what date did the company's only director resign? [Lost the exact description]

A Google search for `cherry software ltd` returns a profile on the [UK's Companies House website](https://find-and-update.company-information.service.gov.uk/) with a registered office address of 4 St. Johns Crescent, Bishop Monkton, Harrogate, North Yorkshire, HG3 3QZ.

<img src="/assets/post3ctf/challenge2cherry.PNG" alt="Cherry Software Limited, 4 St. Johns Crescent, Bishop Monkton, Harrogate, North Yorkshire, HG3 3QZ"/>

We were very stuck on the related by address hint in the challenge description, assuming that meant the questionable business had the same or similar address as Cherry Software LTD.

By searching for companies in Harrogate, we found the company, Tax Fraud LTD:

<img src="/assets/post3ctf/challenge2sketchy.PNG" alt="Tax Fraud LTD result on Companies House website"/>

The company's only director resigned on 11 August 2022.

<img src="/assets/post3ctf/challenge2director.PNG" alt="Director Dylan Sawyer resigned on 11 August 2022"/>

`flag:{11/08/2022}`

### Challenge 3 - Spammy email domain! <a name="challenge3"></a>

*100 points, >=27 solves*

**Challenge Description**: On 11 August, what was the primary email domain from which spam was reported as coming from 185.129.62.62 and 107.189.28.253 (two bot IPs)?

Searching [stopforumspam.com](https://www.stopforumspam.com/) for the IP address 185.129.62.62 returned several spam reports on August 11 for emails under a certain domain.

<img src="/assets/post3ctf/challenge3stopforumspam.PNG" alt="Site results for the search for the IP 185.129.62.62."/>

`flag:{hiroyuki4010.yoshito33.inwebmail.fun}`

### Challenge 4 - A person named Phonenumber <a name="challenge4"></a>
*100 points, >=35 solves*

**Challenge Description**: Wanting to remain anonymous online, discreetly named 'Phonenumber' from Costa Rica has a friend who works for Facebook. When did his friend get married? (MM/DD/YYYY)

A Google search for `"phonenumber" costa rica facebook` returns a [Facebook profile](https://www.facebook.com/phonenumber.phonenumber.39).

<img src="/assets/post3ctf/challenge4facebookprofile.PNG" alt="Phonenumber's Facebook profile"/>

Searching through Phonenumber's friends leads to Dany, who works at Facebook.

<img src="/assets/post3ctf/challenge4friendcensored.png" alt="Phonenumber's friends"/>

Going to Dany's profile shows their marriage date.

<img src="/assets/post3ctf/challenge4friendmarriagecensored.png" alt="Dany's profile w/ marriage date"/>

`flag:{11/03/2007}`

### Challenge 5 - Pool Party, Pt. 1 <a name="challenge5"></a>
*200 points, >=26 solves*

**Challenge Description**: You're investigating a missing person who went missing following a party in 2019. While working through case notes you've come across the following: NTIyMyBTb3V0aCBCcmFlc3dvb2QgQm91bGV2YXJkLCBIb3VzdG9u.  
What date was the pool party?

[Decoding](https://www.base64decode.org/) the base64 encoded string gives an address: 5223 South Braeswood Boulevard, Houston.

A Google search for that address points to a pastebin dump at [https://pastebin.com/BNwRBAX4](https://pastebin.com/BNwRBAX4) containing an email about a party.

<img src="/assets/post3ctf/challenge5pastebin.PNG" alt="Thank you for your RSVP to our mf pool party THIS Saturday."/>

The email headers show that it was sent on 18 April 2019, so the email's reference to "THIS Saturday" would be 20 April 2019.

`flag:{04/20/2019}`

### Challenge 6 - Pool Party, Pt. 2 <a name="challenge6"></a>
*200 points, >=10 solves*

**Challenge Description**: There are two hosts of the party, one is Vanessa, what is the last one of the other host?

<img src="/assets/post3ctf/.PNG" alt=""/>

### Challenge 7 - Callum, Pt. 1 <a name="challenge7"></a>
*100 points, >=14 solves*

**Challenge Description**: Callum lives in Scarborough, Toronto and works with kids. What's his wife's maiden name?

<img src="/assets/post3ctf/.PNG" alt=""/>

### Challenge 8 - Callum, Pt. 2 <a name="challenge8"></a>
*100 points, >=10 solves*

**Challenge Description**: Callum's password has been breached in connection with his primary email. What is it?

<img src="/assets/post3ctf/.PNG" alt=""/>

### Challenge 11 - Eva Hesington <a name="challenge11"></a>
*200 points, >=15 solves*

**Challenge Description**: Hi I'm Eva Hesington. Remember me from last year. I am the founder of Cryptorama. Thanks for your support we have been able to scale the business a lot. I cannot thank the open source community enough. Using Open source tools and platforms, our business has grown and our tech department is now running strong. We could not have done it without these Open Source tools and community. You can visit our website to find out more.

I do indeed remember Eva from [last year's CTF](https://ebristow.com/blog/Recon-Village-CTF-DEFCON-29)!  

todo

<img src="/assets/post3ctf/.PNG" alt=""/>

### Challenge 16 - Find the volcano! <a name="challenge16"></a>
*400 points, >=17 solves*

**Challenge Description**: Can you locate this field on the outskirts of London in the image attached below. Once you do, what date did Doug leave a review for this place? Copy the date from the review as is in the flag format.

<img src="/assets/post3ctf/c16_final.jpg" alt=""/>
<p align="center"><em>Attached image with filename 'c16_final.jpg'</em></p>

There were too many driving ranges in and around London to bother manually searching, so we identified a feature in the picture that stood out.

<p style="text-align:center;"><img src="/assets/post3ctf/challenge16volcano.jpg" alt="Mini golf course with volcano"/></p>

A mini golf course with... perhaps a volcano?

Sure enough, performing a Google search for `london mini golf with volcano` returned [this website](https://hounslowgolfpark.com/) for the Hounslow Golf Park. Notably, the "park" logo poster on the driving range matches the logo on the website.

<img src="/assets/post3ctf/challenge16website.PNG" alt="Screenshot of the Hounslow Golf Park website"/>

There is a Google review left by Doug on July 16 featured on the Hounslow website.

<p style="text-align:center;"><img src="/assets/post3ctf/challenge16dougcensored.png" alt="Screenshot of the Hounslow Golf Park website"/></p>

`flag:{16/07/2022}`

## Honorable Mentions & Conclusion <a name="conclusion"></a>

Jerleneeeeeee :/

Thanks for checking out my writeup! And thanks to those at Recon Village who put together this CTF!