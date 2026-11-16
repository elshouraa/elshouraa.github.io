---
title: xlmrat Lab by CyberDefenders
date: 2026-08-16 00:00:00 +0200
categories:
  - Write-ups
---

hi everyone , anther write-up for lab about my fav platform CyberDefender

[Blue team CTF Challenges | XLMRat — CyberDefenders](https://cyberdefenders.org/blueteam-ctf-challenges/xlmrat/)

Category : Network Forensics

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*0KB5qmRd3Lc-KvhiskdFfg.png)

## **Q1:The attacker successfully executed a command to download the first stage of the malware. What is the URL from which the first malware stage was installed?**

The first thing that came to my mind was that I filtered the HTTP packets, and then I started trying to understand each request :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*gD2WoLH5zUNUxeN0XHvnlA.png)

now, we have two Request from (10.1.9.101) To (45.126.209.4)

TEXT file and IMAGE file

go to follow HTTP stream for IMAGE file “ /mdm.jpg ”:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*GpO0cpNclRSQ2RML71Oa1Q.png)

```
answer : http://45.126.209.4:222/mdm.jpg
```

## **ََQ2:Which hosting provider owns the associated IP address?**

we know associated IP address ( 45.126.209.4 ) , i go to [whatismyipaddress](https://whatismyipaddress.com/) website and search about that :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*p2I8cLETzVVVpgLHwVrq1A.png)

```
answer : Reliablesite.net
```

## **Q3:By analyzing the malicious scripts, two payloads were identified: a loader and a secondary executable. What is the SHA256 of the malware executable?**

by analyzing malicious script in “ /mdm.jpg ” :

i found two scripts:

1- “ $hexString_bbb ”

2- “ $hexString_pe ”

i copy script in “ $hexString_bbb ” and paste in cyberchef:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*qK9iUwseBWbB60wxL7loOw.png)

1- find and replace ( _ )

2- save output as download.dat

theen , i upload this file ( download.dat ) to [virustotal](https://www.virustotal.com/) :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*zTQK60OZnwxmq6V-IJvhMw.png)

```
answer : 1eb7b02e18f67420f42b1d94e74f3b6289d92672a0fb1786c30c03d68e81d798
```

## **Q4:What is the malware family label based on Alibaba?**

by my investigation about this hash

( 1eb7b02e18f67420f42b1d94e74f3b6289d92672a0fb1786c30c03d68e81d798 ) in virustotal i found that:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*KLNSJJiAriQtgi0YTWhSvA.png)

```
answer : AsyncRAT
```

## **Q5:What is the timestamp of the malware’s creation?**

from details section in virustotal :

![](https://miro.medium.com/v2/resize:fit:963/1*7ej0u48sXM5_dt9L4ph-Sw.png)

```
answer :  2023-10-30 15:08
```

# **Q6:Which LOLBin is leveraged for stealthy process execution in this script? Provide the full path.**

LOLBin (Living Off the Land Binaries) refers to legitimate tools or commands within the operating system such as Windows or Linux that can be exploited for malicious purposes, such as executing stealthy processes

# i go to “ /mdm.jpg ” script and search about .exe i found that :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*t5_YkwIDXrzLy2gNirukvA.png)

> after replace # by cyberchef
> 

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*gpttkQPdhW8r2qXFQWy-UQ.png)

we need $VA

```
answer :  C:\Windows\Microsoft.NET\Framework\v4.0.30319\RegSvcs.exe
```

# **Q7:The script is designed to drop several files. List the names of the files dropped by the script.**

in “ /mdm.jpg ” script we have funcation “ WriteAllText ” that do write new file

![](https://miro.medium.com/v2/resize:fit:733/1*90re2_y1YwR4oh1rH9c3ZA.png)

```
answer : Conted.ps1,Conted.vbs,Conted.bat
```

# **Thanks For Reading**

[linkedIn account](https://www.linkedin.com/in/ahmed-elshoura-2a4785193/)
