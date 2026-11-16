---
title: Geolocating Images Walkthrough
date: 2026-10-28 00:00:00 +0200
categories:
  - Write-ups
---

osint challenge from TryHackMe

**Room URL**: [https://tryhackme.com/room/geolocatingimages](https://tryhackme.com/room/geolocatingimages)

Introduction to a guide that will walk you through the "Geolocating Images" room on TryHackMe. The person creating the guide felt like it was similar to another OSINT (Open Source Intelligence) room called "Sakura" that they recently completed. The guide will show you how to find the geographical location of images using OSINT techniques.

# **Task 1: Getting Started**

This tutorial will show you how to geolocate images, from easy things to much harder things.

Our first thought about geolocating images is “where does this image appear on the internet?”

After all, an image may be on a website named “[ILoveEgypt.com](http://iloveegypt.com/)“!

To do this, we use a reverse image searching program. There are many out there on the internet, but the order from how good they are to worst goes:

1. Yandex
2. Yandex
3. Yandex

….

101. Yandex

102. Bing

103. Google

The reason why Google is 103 and not in the first 101 results is that Yandex is a million times better.

Yandex is to Google what a formula 1 racing car is to the $200 car you brought off your friend Ivan who claims the car isn’t stolen but you’ve had police tailing you all week.

It really is night and day. There is no comparison to be made. Use Yandex first, and then a hundred more times. Then after Yandex, use Bing. Then Google. I cannot stress enough how much of a joke Google reverse image search is. **It should be your last resort.**

When you reverse image search with Google, Google tries to find the exact match of that image. With Yandex, it’s almost as if Yandex knows what your image is of straight away and shows you other images of the same thing to reinforce the idea that it knows.

Here’s a fun experiment. Take a picture of yourself right now. You must have other pictures online of yourself. Google reverse image search will likely never find you if you have never uploaded the image.

Yandex can likely work out who you are and show you other images of yourself.

Yandex uses AI to reverse image search, whereas it feels like Google is doing a simple “if IMG_0657 = [Position 1 of image database]: return” against all the images it has.

For more on Yandex vs Bing vs Google, check out Bellingcat’s analysis:

[https://www.bellingcat.com/resources/how-tos/2019/12/26/guide-to-using-reverse-image-search-for-investigations](https://www.bellingcat.com/resources/how-tos/2019/12/26/guide-to-using-reverse-image-search-for-investigations)

**All images needed for this walkthrough are in the zip folder.**

# **Questions**

# **Download the zip file**

> Answer: No answer needed
> 

---

# **Task 2: Getting our feet wet – where is this?**

Where is image 1?

(Use Google Reverse Search and revel in all the airplanes it shows you, which by the way, isn’t the right answer).

Try Yandex Reverse Image search. Look at the differences!

# **Questions**

# **Where in the world is image 1? The answer is the country name.**

Let’s have a look at the image:

![1.jpeg.webp](/assets/img/posts/geolocating-images-walkthrough/1-jpeg.webp)

I used Google reverse image a bunch a had OK results with that, and let’s start with that:

![Screenshot-2025-04-16-at-21.24.44.png.webp](/assets/img/posts/geolocating-images-walkthrough/Screenshot-2025-04-16-at-21-24-44-png.webp)

We got a result on Cloud Gate in Chicago, but on a second look this is NOT the right result:

![image-2-1300x867.png.webp](/assets/img/posts/geolocating-images-walkthrough/image-2-1300x867-png.webp)

Let’s try Yandex instead. Here we get a different result:

![](https://www.jalblas.com/wp-content/uploads/2025/04/Screenshot-2025-04-16-at-21.29.12.png)

Apparently this shows us a sculpture in Karamay, China. After some verification, this seems to be right.

> Answer: China
> 

---

---

# **Task 3: Geolocating Images 101**

Okay, now we know what reverse image searching program to use. Let’s try to actually look at the picture now to figure out where it is!

Let’s say we have a webcam we found on [Shodan.io](http://shodan.io/):

[https://padcam.liverpool.ac.uk/cgi-bin/guestimage.html](https://padcam.liverpool.ac.uk/cgi-bin/guestimage.html)

![](https://github.com/beesecurity/images/blob/master/5.png?raw=true)

**Where is this camera?**

The first thing we notice is the weird crest & title with a black bar (and possibly text) underneath it.

Second thing is the logo, “Kaplan”.

The third thing is that there is a glass building next to a concrete building.

And finally, we have what appears to be a highway next to the glass building. Because it’s a webcam, we can see cars moving quickly!

Putting this into a reverse image search program shows nothing.

Now, something important to note is the name of the webcam. The URL points to [Liverpool.ac.uk](http://liverpool.ac.uk/), which is a university in Liverpool.

If we just had an IP address, we could try to geolocate it using an online tool, checking the ASN number or finding it on Shodan.

Googling “Kaplan University of Liverpool” leads us to a news article about a new building. If we take a look at the image, it looks approximately similar to the one we saw.

Rows of long glasses with a little bit of overhang.

Luckily for us, Liverpool have captioned the image.

`"The proposed new Liverpool International College facility"`

If we google Liverpool International College we get:

[https://www.google.com/maps/place/University+of+Liverpool+International+College/@53.4062447,-2.9625347,17z/data=!4m5!3m4!1s0x487b211eda1b2f5f:0xc226c2ccfb209504!8m2!3d53.4060784!4d-2.9605928](https://www.google.com/maps/place/University+of+Liverpool+International+College/@53.4062447,-2.9625347,17z/data=!4m5!3m4!1s0x487b211eda1b2f5f:0xc226c2ccfb209504!8m2!3d53.4060784!4d-2.9605928)

![](https://www.jalblas.com/wp-content/uploads/2025/04/image-3-1300x867.png.webp)

Which is our building! But it’s not built yet… What gives?

In the bottom right hand corner, Google tells us the image was captured in June 2019.

So Google maps hasn’t updated yet.

If we turn the camera around on Google maps, we can see where the live webcam should be.

Somewhere on this building!

When geolocating an image, we want to point out big landmarks we can easily find on a map. Road layouts, business names, The Empire States Building.

# **Questions**

# **Read the above text**

> Answer: No answer needed
> 

---

---

# **Task 4: Now your turn**

Where was image 2 taken? Specifically, I’m looking for the name of the place that has likely set up the webcam. You’ll know it when you see it!

Please do not use reverse image searches for this!

# **Questions**

# **Where was image 2 taken?**

Alright, the first one was easy with a simple landmark, but let’s try something more realistic. Have a look at the following photo:

![](https://www.jalblas.com/wp-content/uploads/2025/04/2-scaled.png.webp)

We see a large building in the background, and more interestingly, we see a bunch of street signs. We can see `N Sheffield Ave & W Addison St.` In addition, there is a sign for a sport corner, so let’s keep a look out for this.

Anyway, we have an exact crossing with the exact 2 streets:

[`https://www.google.com/maps/place/N+Sheffield+Ave+%26+W+Addison+St,+Chicago,+IL+60613,+USA/@41.9472475,-87.6569009,17z/data=!3m1!4b1!4m6!3m5!1s0x880fd3b2378f06fd:0x7b62c50a69837f8f!8m2!3d41.9472475!4d-87.654326!16s%2Fg%2F11gf37d0yj?entry=ttu&g_ep=EgoyMDI1MDQxMy4wIKXMDSoASAFQAw%3D%3D`](https://www.google.com/maps/place/N+Sheffield+Ave+%26+W+Addison+St,+Chicago,+IL+60613,+USA/@41.9472475,-87.6569009,17z/data=!3m1!4b1!4m6!3m5!1s0x880fd3b2378f06fd:0x7b62c50a69837f8f!8m2!3d41.9472475!4d-87.654326!16s%2Fg%2F11gf37d0yj?entry=ttu&g_ep=EgoyMDI1MDQxMy4wIKXMDSoASAFQAw%3D%3D)

Let’s look at Google Streetview:

![](https://www.jalblas.com/wp-content/uploads/2025/04/Screenshot-2025-04-16-at-21.52.12.png)

This place looks like the right place here the photo has been taken, on the opposite corner. What we see is Wrigley Field, home of the Chicago Cubs. Turn around and you will see that the photo was taken from Wrigleyville Sports.

![](https://www.jalblas.com/wp-content/uploads/2025/04/Screenshot-2025-04-16-at-21.52.37-1300x867.png.webp)

> Answer: Wrigleyville Sports
> 

---

# **Task 5: Helpful tips for geolocating**

Wow, congrats! I found a webcam on [Shodan.io](http://shodan.io/) and took this screenshot, you just geolocated your first image 😎

It’s important to know what is and isn’t likely to be in a country. For example, it is unlikely for a regular Catholic church to appear in places where Budhism / islam is the most popular religeion.

The language used on the shops and vehicles matter too. We can use Google translate to predict what language it could be.

Which side of the road the cars are on, the license plates (you normally can find out what country or state the license plate is from), the markings on the road (different countries have different markings), the style of traffic lights, the clothing choices of those walking around.

To be good at geolocation, we’ve got to open our eyes to all that could be. In your country, for example, it may be common to wear coats during the winter periods. However, in other countries it may not be (think Australia).

Even the smallest of things that we wouldn’t normally think twice about can reveal to us the possible location.

One of the more obvious ways we can geolocate an image is to look at the image details. Does it contain EXIF data?

What about where it was posted – is there a location tagged on social media?

# **Questions**

# **Read the above material**

> Answer: No answer needed
> 

---

# **Task 6: Your turn, again!**

Please do not try to use reverse image searches for this one! Pay close attention to what is in the image.

I want you to answer with the name of the place the webcam is facing.

Note: the name of this location on Google Maps is not the right answer. If you take that location name and paste it back into search, you’ll find out there’s about a million of them. To make this harder, I’m looking for the name that specifically identifies this location. When you enter this name, it’ll be the only one that turns up on Google Maps.

# **Questions**

# **Where was image 3 taken?**

Alright, no reverse image search. Let’s take a look at the picture.

![](https://www.jalblas.com/wp-content/uploads/2025/04/3.png.webp)

We are looking at a large city. The dominant colour seems to be white, and generally there are not many high rises. In the middle of the city (at least from our perspective) we see a river. More importantly, in the background we see a large tower. Many of you will probably suspect that it might be the Eiffel Tower. That means the river in the middle of the city is the Seine, noting the several bridges over the river, which passes close by the Eiffel Tower. If we take into account that the Eiffel Tower is to the right of the river we can conclude that we are actually facing the northeastern direction.

In the foreground we see a dome like structure. Living near to an observatory myself, I immediately recognised it as one. But searching online shows there are quite a few observatories near Paris.

To geolocate the area, we can use the orientation of the observatory relative to the Seine. The river lies roughly in the same southwestward direction as the observatory, though not exactly parallel. It bends slightly, and the direction after the bend also diverges from the line towards the camera. Therefore, the correct direction to search would be at an angle somewhere between two flow directions. A picture makes it more clear:

![](https://www.jalblas.com/wp-content/uploads/2025/04/3-2.png.webp)

And here is a map:

![](https://www.jalblas.com/wp-content/uploads/2025/04/Screenshot-2025-04-17-at-12.59.51.png.webp)

If we follow the orange line we will meet a large green area. If we look at this map on Google earth we can see that there is a Observatory here. Note the observatory (Coupole de la Table Équatoriale

), the building facing the camera, the smaller white structures, and the large tree in between the observatory and the small white structures.

![](https://www.jalblas.com/wp-content/uploads/2025/04/Screenshot-2025-04-17-at-13.10.46.png.webp)

Now compare with the photo:

![](https://www.jalblas.com/wp-content/uploads/2025/04/3-3.png.webp)

So yes, I guess we can conclude that this is the observatory. All we need now is the name. Paris Observatory is not the right name, as this covers three different sites:

[https://en.wikipedia.org/wiki/Paris_Observatory](https://en.wikipedia.org/wiki/Paris_Observatory)

But on the same site we can read that this location is called the Meudon site. The room expects the answer Meudon Observatory to uniquely identify the location.

> Answer: Meudon Observatory
> 

---

# **Task 7: Your turn, what can you see?**

Look at image 4. What do you see? What can you observe?

# **Questions**

# **Where is image 4 taken?**

Alright, final one. Let’s have a look at the final picture:

![](https://www.jalblas.com/wp-content/uploads/2025/04/4.png.webp)

There are a few things that immediately came to my attention. The first detail is that people drive on the left side of the street. That significantly reduces the number of countries to countries with a greater historic British influence which this map shows (left-driving countries show in blue):

![](https://www.jalblas.com/wp-content/uploads/2025/04/image-1-1300x867.png.webp)

Another element I was unsure with were the poles with yellow globes on top. After some searching I found out that these are called Belisha beacons. These mark pedestrian road crossings:

[https://en.wikipedia.org/wiki/Belisha_beacon#:~:text=A%20Belisha%20beacon%20(%2Fb%C9%99,Malta%2C%20New%20Zealand%20and%20Singapore.](https://en.wikipedia.org/wiki/Belisha_beacon#:~:text=A%20Belisha%20beacon%20(%2Fb%C9%99,Malta%2C%20New%20Zealand%20and%20Singapore.)

Fun fact: *The first Belisha beacons were erected in the London authorities areas and, following the Road Traffic Act 1934, were rolled out nationally in 1935. In December 1941, a study was made into the cost effectiveness of melting down the 64,000 Belisha beacon posts to make munitions, a plan which threatened to “deprive the right hon. Member for Devonport (Mr. Hore-Belisha) of his last hope of immortality.”*

Anyway, these are mostly found in England, but again also show up in other countries with a great English influence. The buildings and cars do look very english though! But we still do not have a more specific location.

I decided to use Yandex to image search the image, and wow! A lot of results showed up.:

[https://yandex.com/images/search?cbir_id=2782173%2FsVniwdn_aTepRQhrtfv6zw8748&cbir_page=similar&lr=105288&rpt=imageview&url=https%3A%2F%2Favatars.mds.yandex.net%2Fget-images-cbir%2F2782173%2FsVniwdn_aTepRQhrtfv6zw8748%2Forig](https://yandex.com/images/search?cbir_id=2782173%2FsVniwdn_aTepRQhrtfv6zw8748&cbir_page=similar&lr=105288&rpt=imageview&url=https%3A%2F%2Favatars.mds.yandex.net%2Fget-images-cbir%2F2782173%2FsVniwdn_aTepRQhrtfv6zw8748%2Forig)

An example here:

![Abbey Road](https://www.jalblas.com/wp-content/uploads/2025/04/Screenshot-2025-04-16-at-20.41.31.png)

Abbey Road

A ton of the results mention Abbey Road (in London), a name you might know from the Beatles. And yes, it is apparantely the exact same spot where the Beatles album cover was made:

*Abbey Rd., London NW8 9DD, United Kingdom*

The album cover just faces the other way.

![](https://www.jalblas.com/wp-content/uploads/2025/04/Screenshot-2025-04-16-at-20.59.49-1300x867.png.webp)

And actually, the gate you see in the right is part of the Abbey Road Studios:

![](https://www.jalblas.com/wp-content/uploads/2025/04/Screenshot-2025-04-16-at-20.57.06-scaled.png.webp)

Anyway, the answer is Abbey Street.

> Answer: Abbey Street
> 

---

# **Task 8: You’re done!**

And that’s it!

Check out Bellingcat for more on geolocation:

[https://www.bellingcat.com/news/2020/01/21/geolocating-venezuelan-lawmakers-in-europe](https://www.bellingcat.com/news/2020/01/21/geolocating-venezuelan-lawmakers-in-europe)

Alternatively, play a lot of Geoguesser!

[https://geoguessr.com](https://geoguessr.com/)

# **Questions**

# **Check out the links above!**

> Answer: No answer needed
> 

---

# **Congratulations on completing Geolocating Images!!!**
