---
title: EscapeRoom Lab by CyberDefenders
date: 2026-10-01 00:00:00 +0200
categories:
  - Write-ups
---

hi everyone , anther write-up for lab about my fav platform CyberDefender

[Blue team CTF Challenges | EscapeRoom — CyberDefenders](https://cyberdefenders.org/blueteam-ctf-challenges/escaperoom/)

![](https://miro.medium.com/v2/resize:fit:653/1*en_QySs4bRg__sH2JGT1Fg.png)

## **Q1:What service did the attacker use to gain access to the system?**

i use (WireShark) to open file go to view statistics —> -→ open protocol hierarchy statistics. We See More Traffic Through the SSH Protocol.

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*qcroK_s6cY5YvbT2.png)

```
answer : SSH
```

## **Q2:What attack type was used to gain access to the system?**

During my investigation, i observe a high volume of network traffic using the *SSH protocol* . The attacker is employing a brute-force technique to try and gain access.

```
answer : bruteforce
```

## **Q3:What was the tool the attacker possibly used to perform this attack?**

by my search i get that “ Hydra is a very common and popular tool used for brute-force attacks ”

```
answer : Hydra
```

## **Q4:How many failed attempts were there?**

i use Brim’s Zui to See Clearly Statistics about failed attempts

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*CKDV9aMrWqd8f4Ug7Jn59Q.png)

now i have 52 failed attempts from 2 true attempts

```
answer : 52
```

**Q5: What credentials (username: password) were used to gain access? Refer to shadow.log and sudoers.log**

`john - wordlist=/usr/share/wordlists/rockyou.txt shadow.log`Press enter or click to view image in full size

`answer : manager:forgot`

![](https://miro.medium.com/v2/resize:fit:963/1*x2G5ZTqPEC4ZiF_prOnvLQ.png)

## **Q6: What other credentials (username:password) could have been used to gain access also have SUDO privileges? Refer to shadow.log and sudoers.log**

now i open “ sudoers.log ” file

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*NtcndZO_ANgZxOTDZEUB7g.png)

# The statement “ **ALL=(ALL) ALL ”** means that the user has full privileges to run any command as root

and i have usernames and their passwords :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*j40g8Cgi6ZDMb94v8ObTaw.png)

```
answer :   sean:spectre
```

## **Q7:What is the tool used to download malicious files on the system?**

back to Wireshark , ” The first thing that came to my mind was to use the filter ” (ip.addr==10.252.174.188) && (_ws.col.protocol == “HTTP”) ” to search for the HTTP packets coming from a specific IP that I identified from the endpoints list ”

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*rBhP5gMGkmDY1mxHj0UJDQ.png)

# I noticed something strange here from “ *User-Agent: Wget/1.13.4 (linux-gnu)\r\n ”*

and i search about this wget user-agent

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*_FXGA_qxWBC_8n7swdIvAA.png)

```
answer :  wget
```

## **Q8:How many files the attacker download to perform malware installation?**

> The first thing that came to my mind about files was going to File → export files → http… → content type = text/html
> 

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*9oRgXKMOKuKPxkpGEfL7SA.png)

now we have 3 files ,They were all sent from the same IP address

```
answer :  3
```

## **Q9:What is the main malware MD5 hash?**

go to vmware go pervious steps and Save all 3 Files and 1.html

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*uy9pghUXzkWM8rl4TEGq4w.png)

```
answer :  772b620736b760c1d736b1e6ba2f885b
```

## **Q10:What file has the script modified so the malware will start upon reboot?**

when i open 3.html i find that :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*2E_1BM380at1yycBpQ8SBA.png)

This script shown in the image is **malicious or suspicious**, likely part of a **persistence mechanism for malware** in a Linux system

```
answer: /etc/rc.local
```

## **Q11:Where did the malware keep local files?**

From our analysis of the shell script, it copies the main payload to the `/var/mail` directory

```
answer: /var/mail/
```

## **Q12:What is missing from ps.log?**

*Where did the malware apply its changes here?* Open ps.log File and Investigae in it i Doesn’t Find /var/mail/mail This Path The Malware Keep local Files

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*HadNplwajrB8S3oKmw1SEw.png)

```
answer : /var/mail/mail
```

## **Q13:What is the main file that used to remove this information from ps.log?**

back to 3.html , i found this :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*CI6r_gqdGdMiKD-vLjUVmQ.png)

```
answer: sysymod.ko
```

**Q14:Inside the Main function, what is the function that causes requests to those servers?**

`answer: requestFile`

## **Q15:One of the IP’s the malware contacted starts with 17. Provide the full IP.**

by going to networkminer → Hosts :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*CFWkXHbrH-pP-ftwVPvbKQ.png)

```
answer: 174.129.57.253
```

Q16:How many files the malware requested from external servers?

frist thing , i notice that:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*vCTD2Np4Cr0NrsxB0KNtlQ.png)

3 malicious servers connect with malware

next , i go to Files :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*EfClMSYcqbUMbNnYTQIfHw.png)

we have 9 files

```
answer: 9
```

## **Q17:What are the commands that the malware was receiving from attacker servers? Format: comma-separated in alphabetical order**

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/0*UbMpCqhWZUBx94pZ.png)

Use Any Online Platform To Converted We Use (CyberChef)

![](https://miro.medium.com/v2/resize:fit:612/0*bXUMkctq_wFaFPB5.png)

```
answer : NOP,RUN
```

## **Thanks For Reading**
