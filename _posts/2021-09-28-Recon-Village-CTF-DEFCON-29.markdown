---
layout: post
title:	"Recon Village CTF Writeup"
date:	2021-09-28 23:22:01 -0700
categories: OSINT CTF
---
On August 6th and 7th, I had the pleasure of participating in DEFCON 29's [Recon Village](https://www.reconvillage.org/index.html) Capture the Flag competition. It was my first time competing, and it was a lot of fun! Team Trojan placed 8th, and I placed 5th out of 240 registered participants individually. 

![Team Trojan's score breakdown](/assets/post1ctf/8me.PNG)

The challenges were difficult, with many still unsolved at the end of the two-day competition. Congrats to teams **unremarkable**, **QultOftheQuantumQow**, and **pinja** for being the top 3 teams!

![Top 10 teams score plot](/assets/post1ctf/Top10Teams.png)

This informal writeup covers solutions for Challenge 14, Challenge 15, and Challenge 16. Though I did not solve Challenge 17, I made some progress and it was still unsolved by the end of the competition so I am including a few notes on it too.

## Challenge 14
*200 points, 31 solves*

**Challenge Description**: We lost our contact with Mr. Sanjeev Shah Tolia. We made a website for him but lost his registered street address. Can you find it for us?

This challenge was amusing because the first address I discovered through a Google search seemed so perfect that I fruitlessly attempted to enter it for at least ten minutes.

<img src="/assets/post1ctf/honeypot.PNG" alt="Sanjeev Shah Tolia incorrect address: Devonshire House 582 Honeypot Lane, Stanmore"/>

582 **Honeypot** Lane! Of course, seeing an address with a computer security term in it made me think I'd struck gold. But a [honeypot](https://en.wikipedia.org/wiki/Honeypot_(computing)) is a trap intended to lure and trick attackers - and in this case, I was the one being tricked! Assuming I am correct, this was a clever and funny addition by the developers of this CTF.

After trying another Google search string or two, I found a plausible (albeit less exciting) address that was the correct answer.

<img src="/assets/post1ctf/7London.PNG" alt="The correct address - 7 London Road"/>


flag:{7 London Road}


## Challenge 15
*200 points, 20 solves*

**Challenge Description**: We were provided with the below image named Recruited.png

<img src="/assets/post1ctf/Recruited.png" alt="Picture of Eva Hesington's Company ID with a QR Code" height="300"/>

Uploading the QR code to [webqr.com](https://webqr.com) displayed this electronic business card (vCard):

```
BEGIN:VCARD VERSION:3.0 N:Hesington;Eva;;; FN:Eva Hesington 
ORG:CryptoRama EMAIL;type=INTERNET;type=WORK;type=pref:eva@cryptorama.xyz
URL;type=WORK;type=pref:https://eva.cryptorama.xyz
TEL;type=CELL;type=VOICE;type=pref:+19876543210 END:VCARD
```

Eva Hesington's website, **https://eva.cryptorama.xyz**, was a simple single-page UIdeck resume site. There was a clickable button titled **Download Resume**:

<img src="/assets/post1ctf/downloadResume.PNG" alt="About me section with the Download Resume button"/>

When I initially loaded the resume, I noticed that there was a code that flashed on the left side of the document but quickly disappeared. Starting a video before refreshing the page allowed me to capture this video frame displaying the flag:

<img src="/assets/post1ctf/resume_flag.PNG" alt="About me section with the Download Resume button"/>

flag:{h!$st0r4\_i$\_b@D}


## Challenge 16
*427 points, 2 solves*

**Challenge Description**: Unfortunately failed to archive the description, but I know it included the hint "this challenge will not be a walk in the park".

And when I read that this challenge would not be a walk in the park, I remembered something from Eva Hesington's about me section - she likes going on walks with her husband to a nearby park.

<img src="/assets/post1ctf/bio.PNG" alt="About me section, she likes to go on walks in the park"/>

There was also a map at the bottom of the webpage.

<img src="/assets/post1ctf/peartree.PNG" alt="Google map with Peartree Apartments pinned"/>

I thought that the most logical location for the flag would be a Google or Yelp review left by Eva Hesington for a park within walking distance of Peartree Apartments. I started searching reviews for "Eva" in case she used a different last name outside of work. After trying many parks' review pages including Washington Park, Murphy Park, Cannery Park, Columbia Park, and Ponderosa Park I decided to take a break on this challenge. 

Next, I decided to comb through the website's HTML using [page source](https://computer.howstuffworks.com/web-page2.htm).

<img src="/assets/post1ctf/pageSource.PNG" alt="Page source showing that Eva Hesington's husband's name was hidden"/>

Look closely at the HTML for this section of the webpage. We saw earlier that Eva Hesington's relationship status was "Married". The page source above revealed that her husband's name, John Graham, was set to "display: none" so it was hidden from view on her website. Instead of saying "Relationship: Married", the page actually said "Relationship: Married to John Graham".

On the Yelp page for [Washington Park](https://www.yelp.com/biz/washington-park-sunnyvale), reviewer John G. left a flag! 

<img src="/assets/post1ctf/WashingtonPark.PNG" alt="John Graham's Washington Park review"/>

flag:{d0nT_b3_fr!EndL4_w!tH_stR@nGeRs}

Note: It might seem unrealistic for extra information to be hidden in a webpage. After all, secure databases exist for a reason! But look no further than this ethical hacker's discovery of a former [Australian Prime Minister's passport number and phone number](https://www.theguardian.com/australia-news/2020/sep/16/former-australian-pm-tony-abbotts-passport-details-and-phone-number-obtained-by-hacker) stored on an airline's website. Yikes.

## Challenge 17 (unsolved)
*\~500 points, 0 solves*

**Challenge Description**: The third and final part of the Eva Hesington-related problems (Challenges 15, 16, and 17). Failed to archive this one as well, but I remember the description being unhelpful. I found the filepath clue below by enumerating every filepath on the site, not through any hint here.

Opening one of the website's images in a new tab and looking at its filepath gave a hint.

<img src="/assets/post1ctf/evaGitlabHint.PNG" alt="Image from site with AWS filepath"/>

/**find/me/on/gitlab**/about-2.jpg 

There was an email address listed under contact information on Eva Hesington's site: eva.hesington.1213@gmail.com. Username **eva.hesington.1213** returned a registered GitLab user.

<img src="/assets/post1ctf/gitlabuser.PNG" alt="GitLab search showing Eva's profile under the username eva.hesington.1213"/>

There was a repository called My Personal Website. Cloning the repository and opening index.html revealed a website almost identical to the eva.cryptorama.xyz site. 

<img src="/assets/post1ctf/repo.PNG" alt="Screenshot showing the repository in GitLab"/>

The file account.txt in the repository contained an [AWS](https://console.aws.amazon.com/console/home?nc2=h_mo) Account ID and an EC2 Instance type. But I could not find nor guess the password, so I became stuck at this point.

<img src="/assets/post1ctf/account.PNG" alt="showing contents of account.txt in the repository, ID 727048636561 and EC2 Instance t3.medium"/>

I also tried using the [Diff Checker website](https://www.diffchecker.com/) to examine the difference in the HTML for eva.cryptorama.xyz and index.html in the GitLab repository. There were a few small changes - the new index.html page had **evahesington@gmail.com** in place of **eva.hesington.1213@gmail.com**. Unfortunately, this discovery did not help further my progress.

<img src="/assets/post1ctf/contact.PNG" alt="Eva Hesington's contact infomation for the index.html file"/>

## Conclusion

Note - I did score 827 points (200, 200, and 427), but I "bought" a hint using 50 points bringing my total down to 777 (and didn't even end up making any notable progress on that challenge, oh well)

Thanks for checking out my writeup! And thanks to those at Recon Village who put together this CTF!