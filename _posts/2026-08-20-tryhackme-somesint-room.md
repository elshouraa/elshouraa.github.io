---
title: TryHackMe somesint room
date: 2026-08-20 00:00:00 +0200
categories:
  - Write-ups
---

introduction,

“ Despite some initial challenges and errors in the preparation process, I found this lab to be an incredibly valuable experience. It provided me with hands-on practice in OSINT, further strengthening my skills in this field. ”

room link : [TryHackMe | KaffeeSec — SoMeSINT](https://tryhackme.com/room/somesint)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*funIl2JKl0rYm2fy.jpeg)

task 2 || story

after you read the story that talked about your hired in this mission and understand well.

## **1.Who hired you?**

```
ks{H}
```

## **2.Who are you investigating? ( ks{ firstname lastname } )**

```
ks{thomas straussman}
```

task 3 || Let’s get started!!

## **1.What is Thomas’ favorite holiday?**

after apply this google dork :-

> “ username ”thomas straussman” ”
> 

i found account on twitter named : -

> Thomas Straussman (Ø,G)
> 
> 
> *@TStraussman*
> 

and he from greenland

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*GamIieY2w_RUk5zh-fFQCg.png)

after understand his bio well the answer :-

```
Christmas
```

## **2.What is Thomas’ birth date?**

by search about tstraussman on google i found another account on Riddit.com and in his bio , there is link to Twitter account

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*5OHLw47yddpmxQGQ45CQhQ.png)

Looks like he joined in Dec 19, 2020

next step view his image :-

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*qOmmTZ0Zdpj8Hq88FOZEtg.png)

in this post , There is no information about his birth date, so i go to source code for search about any date:-

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*ws5Upup0p4G7cfgH5qjD5A.png)

The time the post was published was 2020–12–20, and the person was celebrating their 30th birthday, so they were born on 1990–12–20.

```
12-20-1990
```

## **3. What is Thomas’ fiancee’s Twitter handle?**

after search about “site:twitter.com “Francesca Hodgerint” ” in google i found acount in X.com :-

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*4gT1COJCRScbk5cxgRgKNA.png)

```
@fhodgelink
```

## **4.What is Thomas’ background picture of?**

after inverse the background picture on google :-

![](https://miro.medium.com/v2/resize:fit:558/1*anTdYJOQr-UaDNNveqF-Dg.png)

```
Buddha
```

Task 4 | Spider… what?

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*YChtgzGd4r82MY1J.png)

At this point I ended up having issues with cherry.py and a bunch of other things (I was using the TryHackMe attack box), but I was able to Google my way through them using the error messages to eventually get to this:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*xXkbWkaEhhJMZtL_.png)

Then I pulled up the instance in a browser:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*AqrhE4CTl2L8zJof.png)

I started setting up a new scan:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*nF6rNM-1tpG3rufl.png)

Here are the results:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*9v67tQA8GrQV6RHo.png)

You can see this picked up the same things as Google did earlier:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*LMM25FLyXFG7WssQ.png)

## **1. What was the source module used to find these accounts?**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*eBmLezsg6EeOyDko.png)

```
sfp_accounts
```

## **2. Check the shadowban API. What is the value of “search”?**

Click on the Twitter result and it will open up this in a new tab:

![](https://miro.medium.com/v2/resize:fit:600/0*nR7jYYdY4ftnLBIS.png)

```
ks{1346173539712380929}
```

task 5 || Connections, connections..

## **1.Where did Thomas and his fiancee vacation to?**

I found this photo on francesca account :-

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*W8PYTYMdf6_GxwowA_5z_A.png)

and by some inverse this photo I have reached the site location

![](https://miro.medium.com/v2/resize:fit:553/1*nr3Vc8ZFOhxf2vmj_poc3Q.png)

```
Koblenz, Germany
```

## **2.When is Francesca’s Mother’s birthday? (without the year)**

i found this tweet :-

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*OGXuaV4zdMRSn1dGZccV6g.png)

```
December 25th
```

## **3.What is the name of their cat?**

i found this tweet :-

![](https://miro.medium.com/v2/resize:fit:793/1*uTQWX-3_y_MFCAGHnOEc4g.png)

```
gotank
```

## **4.What show does Francesca like to watch?**

i found this tweet :-

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*_bvDxmGgl19IVl32Wjmmvg.png)

```
#90 day fiancee
```

task 6 || Turn back the clock!!

## **1.What is the name of Thomas’ coworker?**

This is the time web archives by [https://web.archive.org](https://web.archive.org/)

frist i try by link Tstraussman’s post on Reddit :- “[https://www.reddit.com/user/Tstraussman/comments/kh1pzg/big_thank_you/](https://www.reddit.com/user/Tstraussman/comments/kh1pzg/big_thank_you/) ”

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*a3D-MgLdlm5w2e3uaXJJ9Q.png)

i found two archives saved since late 2020 ( **December 21, 2020** )

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*rNdYLypipkI6s-uz.png)

His username is /minikhans. From this we can deduce his full name

## **2.Where does his coworker live?**

i have username of his coworker on Reddit “ [/minikhans](https://www.reddit.com/user/minikhans/comments/) ”

then i read his bio :-

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*UpaKdAC0IpIYw4QvPoHI-A.png)

```
Nuuk, Greenland
```

## **3.What is the paste ID for the link we found? (flag format)**

at 23 mar 2021 page saved and i found link :-

![](https://miro.medium.com/v2/resize:fit:696/0*H9skB0MkItm4BOIV.png)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*6QRfkeJny9ew2niJ.png)

![](https://miro.medium.com/v2/resize:fit:792/0*ncOZMHQLyNlK_icO.png)

```
ks{ww4ju}
```

## **4.Password for the next link? (flag format)**

![](https://miro.medium.com/v2/resize:fit:402/1*xyEhHebMkrcuL0NfL3dBbw.png)

```
1qaz2wsx
```

## **5.What is the name of Thomas’ mistress?**

```
Emilia Moller
```

## **6.What is Thomas’ Email address?**

![](https://miro.medium.com/v2/resize:fit:601/0*2MeXwmah3uDt0JfV.png)

```
straussmanthom@mail.com
```

finish……...

**Thanks for reading … *😊😊***
