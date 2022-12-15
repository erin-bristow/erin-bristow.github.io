---
layout: post
title:	"DEF CON 30 - Recon Village CTF Writeup"
date:	2022-08-18 12:00:00 -0700
categories: OSINT CTF
---
After spending Friday of our first (!!) in-person DEF CON wandering around, on Saturday my friend [Jeffrey](https://github.com/j-hertzog) and I decided to settle down in the [Recon Village](https://www.reconvillage.org/index.html) and work on their CTF for a few hours. Team Trojan tied for 4th out of 59 teams.

# Table of Contents
1. [DEF CON!](#defcon)
2. [Writeup Intro](#writeup-intro)
3. [Challenges](#challenges)
	- [Challenge 2 - Tax Fraud LTD.](#challenge2)
	- [Challenge 3 - Email spam!](#challenge3)
	- [Challenge 4 - A person named Phonenumber](#challenge4)
	- [Challenge 5 - Pool Party, Pt. 1](#challenge5)
	- [Challenge 6 - Pool Party, Pt. 2](#challenge6)
	- [Challenge 7 - Callum, Pt. 1](#challenge7)
	- [Challenge 8 - Callum, Pt. 2](#challenge8)
	- [Challenge 11 - Eva Hesington](#challenge11)
	- [Challenge 16 - Find the volcano!](#challenge16)
4. [Conclusion](#conclusion)


## DEF CON! <a name="defcon"></a>
Feel free to skip straight to the [writeup intro](#writeup-intro), but I wanted to write a little about my experience at the conference too. 
At long last, an in-person DEF CON that I could attend! Had the best time with old friends and new friends. :)

I went with two friends from USC and we stayed at Tuscany Suites & Casino about a ten minute walk from the conference. 

<p style="text-align: center;" align="center"><img src="/assets/post3ctf/friends.jpg" alt=""/></p>
<p align="center"><em>Jeffrey, Diba, and me - very tired on the last day of the conference :,)</em></p>

Hacker jeopardy was definitely one of the highlights of the conference. Never in my life have I seen more [beach balls](https://twitter.com/c4i/status/1559633675117121537?s=20&t=u4MGGZqo4CPtuGwxTGIuXA). At the beginning, we had to wait a few minutes for the Caesars Forum employees to bring the beer cart... because in addition to points for answering questions correctly, you also get points for each bottle of beer you drink??

<p style="text-align:center;" align="center"><img src="/assets/post3ctf/hacker-jeopardy.gif" alt="a beach ball flies by a screen that says 'The people responsible have been sacked. Everyone please... SIT THE FUCK DOWN!'"/></p>
<p align="center"><em>Waiting for the beer people!</em></p>

Some of the categories included: <em>Are you smarter than a CSSLP?</em>, <em>pandemodem</em>, <em>little green padlocks</em>, and <em>NFT: No Fucking Thanks</em>. Many questions involved pieces of [hacker culture](https://en.wikipedia.org/wiki/Hacker_culture) and DEF CON history while others asked networking questions like which service uses which port ([TELNET](https://twitter.com/HackerJeopardy/status/1563780446445621248), anyone?). 

Other highlights:
- Met some awesome hackers at the Double Down Saloon on the last night of the conference
- Was offered to join the Church of WiFi but the [initiation process](https://twitter.com/cydefe/status/1528586303264149505?s=20&t=cycMCUmuOJ9jbqONpHnDxA) seemed a little intimidating... maybe next year hehe
- the Recon Village CTF!!

## Writeup Intro <a name="writeup-intro"></a>

Last year's challenges were more difficult. Many went unsolved, and Team Trojan secured 8th place with only three solves. This year, we solved nine challenges and tied for 4th! We had a great time competing, so a big thanks to the organizers of the CTF.

![Scoreboard](/assets/post3ctf/top5.PNG)
<p align="center"><em>Graph showing the progress of the Top 10 Teams</em></p>

The CTF began on Friday and we started on Saturday so we had a bit of catching up to do (in the above graph, we're the purple line that started second-to-last!).

![Challenges we solved and the time when each challenge was solved](/assets/post3ctf/challengesSolved.png)
<p align="center"><em>Our solved challenges with timestamps</em></p>

Notes:
1. This CTF included profiles and online information for real people. Therefore, some information has been redacted in this writeup.
2. The number of solves for each challenge is the number when we first solved that challenge. We did start late, so there weren't too many solves after us.

## Challenges <a name="challenges"></a>

### Challenge 2 - Tax Fraud LTD. <a name="challenge2"></a>
*100 points, ~45 solves*

**Challenge Description**: Cherry Software LTD is associated by address with a questionable business registered on August 4th. On what date did the company's only director resign? [This is paraphrased - lost the exact description]

A Google search for `cherry software ltd` returns a profile on the [UK's Companies House website](https://find-and-update.company-information.service.gov.uk/) with a registered office address of 4 St. Johns Crescent, Bishop Monkton, Harrogate, North Yorkshire, HG3 3QZ.

<img src="/assets/post3ctf/challenge2cherry.PNG" alt="Cherry Software Limited, 4 St. Johns Crescent, Bishop Monkton, Harrogate, North Yorkshire, HG3 3QZ"/>

We were very stuck on the "associated by address" hint in the challenge description, assuming that meant the questionable business had the same or similar address as Cherry Software LTD.

By searching for other companies in Harrogate, we found the company, Tax Fraud LTD:

<img src="/assets/post3ctf/challenge2sketchy.PNG" alt="Tax Fraud LTD result on Companies House website"/>

The company's only director resigned on 11 August 2022.

<img src="/assets/post3ctf/challenge2director.PNG" alt="Director Dylan Sawyer resigned on 11 August 2022"/>

`flag:{11/08/2022}`

### Challenge 3 - Email spam! <a name="challenge3"></a>

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

[Decoding](https://www.base64decode.org/) the base64 encoded string gives an address in Houston.

A Google search for that address points to a pastebin dump at [https://pastebin.com/BNwRBAX4](https://pastebin.com/BNwRBAX4) containing an email about a party.

<img src="/assets/post3ctf/challenge5pastebin.PNG" alt="Thank you for your RSVP to our mf pool party THIS Saturday."/>

The email headers in the pastebin dump show that it was sent on 18 April 2019, so the email's reference to "THIS Saturday" would be 20 April 2019.

`flag:{04/20/2019}`

### Challenge 6 - Pool Party, Pt. 2 <a name="challenge6"></a>
*200 points, >=10 solves*

**Challenge Description**: There are two hosts of the party, one is Vanessa, what is the last one of the other host?

The email says that anyone "on Meghana's or Vanessa's invite list can come in for free." From this, we assumed that Meghana was the other host. 

The pastebin dump included the entire email including headers and the "from" field, so we had about 80 full names and email addresses. Searching Facebook for a few of these names returned one that was friends with Meghana.

<img src="/assets/post3ctf/challenge6profilefriendcensored.png" alt="a Facebook profile, with faces/names pixelated"/>

<img src="/assets/post3ctf/challenge6profilecensored.png" alt="a Facebook profile, with faces/names pixelated"/>

`flag:{lastname}`

### Challenge 7 - Callum, Pt. 1 <a name="challenge7"></a>
*100 points, >=14 solves*

**Challenge Description**: Callum lives in Scarborough, Toronto and works with kids. What's his wife's maiden name?

Googling `callum scarborough toronto` led us to a LinkedIn profile of someone named Callum that got a diploma in childcare. 

<img src="/assets/post3ctf/challenge7linkedincensored.png" alt="Callum's LinkedIn profile"/>

Searching Facebook for his full name returned a profile with a "Married to" section linked to another Facebook profile (unfortunately with the same last name).

<img src="/assets/post3ctf/challenge7facebookhusbandcensored.png" alt="Callum's Facebook profile"/>

But when Ashley first created a Facebook account, it was likely under her maiden name. As a result, that original name was visible in the URL. 

<img src="/assets/post3ctf/challenge7facebookurlcensored.png" alt="Ashley's Facebook profile"/>

`flag:{lastname}`

### Challenge 8 - Callum, Pt. 2 <a name="challenge8"></a>
*100 points, >=10 solves*

**Challenge Description**: Callum's password has been breached in connection with his primary email. What is it?

A Google search for `site:pastebin.com callum lastname` returns a dump containing an email password combo that belongs to Callum. 

`flag:{password}`

### Challenge 11 - Eva Hesington <a name="challenge11"></a>
*200 points, >=15 solves*

**Challenge Description**: Hi I'm Eva Hesington. Remember me from last year. I am the founder of Cryptorama. Thanks for your support we have been able to scale the business a lot. I cannot thank the open source community enough. Using Open source tools and platforms, our business has grown and our tech department is now running strong. We could not have done it without these Open Source tools and community. You can visit our website to find out more.

I do indeed remember Eva from [last year's CTF](https://ebristow.com/blog/Recon-Village-CTF-DEFCON-29)! Eva appears to be a fictional person created for this CTF, so full detailed are being included for this challenge. 

With Firefox Developer tools, we found `dist/js/main.min.js` which had a comment reminding someone to remove a token before the code was pushed to production.

<img src="/assets/post3ctf/challenge11javascript.PNG" alt="JavaScript with commented token"/>

`flag:{d0_N0t_cOd3_&_c0mM3nt}`

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

## Conclusion <a name="conclusion"></a>

Thanks for checking out the writeup, and thanks to those at Recon Village who put together this CTF.

[Here's the writeup](https://andrew.cloud/blog/dc30-writeup/) from the winning team if you'd like to look at additional solves!