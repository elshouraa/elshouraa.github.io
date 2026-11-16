---
title: Acoustic challenge write-up
date: 2026-10-20 00:00:00 +0200
categories:
  - Write-ups
---

LEVEL : Medium

from cyberdefenders

[Blue team CTF Challenges | Acoustic — CyberDefenders](https://cyberdefenders.org/blueteam-ctf-challenges/acoustic/)

— — — — — — — — — — — — — — — — — — — — — — —

### **Scenario**

![](https://miro.medium.com/v2/resize:fit:437/1*PR3YNc7hXDy0R9fxprDsvg.png)

This lab takes you into the world of voice communications on the internet. VoIP is becoming the de-facto standard for voice communication. As this technology becomes more common, malicious parties have more opportunities and stronger motives to control these systems to conduct nefarious activities. This challenge was designed to examine and explore some of the attributes of the SIP and RTP protocols.

**files**

log.txt || Voip-trace.pcap

## **Q1-What is the transport protocol being used?**

look at wireshark and see protocols go to “ statistics > protocol hierarchy “ :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*jHThwIfbRaF-P8mSb4tcLA.png)

The Session Initiation Protocol (SIP) and Real-time Transport Protocol (RTP) both utilize the **User Datagram Protocol (UDP)**

```
the answer is UDP.
```

## **Q2-The attacker used a bunch of scanning tools that belong to the same suite. Provide the name of the suite**

You will notice that when you anlysis frist packet:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*Rkmz9LzHAQoktuvcnLjPNQ.png)

when you search on this “ sipvicious” on google :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*_kwxXwMquUpAz0qDk6361A.png)

```
THE Answer : SIPVicious
```

## **Q3-What is the User-Agent of the victim system?**

To complete the packet analysis, we will find:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*3ll9EyqIzk3tSbVFltPCJw.png)

```
THE Answer : Asterisk PBX 1.6.0.10-FONCORE-r40
```

## **Q4-Which tool was only used against the following extensions: 100,101,102,103, and 111?**

When we dig deeper into sipvicious we find that SIPVicious OSS is a VoIP security testing toolset. It helps security teams and has a repository in GitHub [https://github.com/EnableSecurity/sipvicious/tree/master/sipvicious](https://github.com/EnableSecurity/sipvicious/tree/master/sipvicious)

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*z0q7a82jgSgU5ivTAaq-tQ.png)

Now we have 6 files and when we delve into searching for the goals and purpose of each file with the help of deepseek:

svmap.py — Scan the network for active SIP devices.

svwar.py— Identifies a valid SIP account by testing the username.

svcrack.py — Brute-force attack to find SIP passwords.

svreport.py — Manage and export results reports from the above tools.

svcrash.py — An experimental attack tool to crash or crash the SIP service.

```
THE Answer : svcrack.py
```

## **Q5-Which extension on the honeypot does NOT require authentication?**

After applying the protocol “sip” in WIRESHARK filter :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*qKImNzlQkw38YujibbmYVg.png)

We will find a successful connection with the extension 100 without any authentication

```
THE Answer : 100
```

## **Q6-How many extensions were scanned in total?**

i used this command to get the answer:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*wrBIgYfsSIyZE_DGOFYkhw.png)

```
THE Answer : 2652
```

## **Q6-How many extensions were scanned in total?**

i used this command to get the answer:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*56cq21cWgmW6pjKocAEC1w.png)

```
THE Answer : zoiper rev.6751
```

## **Q8-Multiple real-world phone numbers were dialed. Provide the first 11 digits of the number dialed from extension 101?**

“ The `INVITE` request is sent by a SIP client (e.g., a phone or scanner) to **start a call** or session with another SIP device (e.g., extension `101`) ”

i used this command to get the answer:

```
grep -i 'INVITE' -A3 log.txt | grep sip
```

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*o65OVuDSI-4GdxMHwwY3EA.png)

We will find in the previous screen that What was the most recent 11-digit number dialed is 00112524021

```
THE Answer : 00112524021
```

## **Q9-What are the default credentials used in the attempted basic authentication? (format is username:password)**

I use a website called “ apackets” to analyze the pcap files

```
https://apackets.com
```

go to [Credentials](https://apackets.com/pcaps/creds) section :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*4mKvouEsulrnopkjDmOmOw.png)

```
THE Answer : maint:password
```

or second solve by analysis packets manual in wireshark

## **Q10-Which codec does the RTP stream use? (3 words, 2 spaces in between)**

filter the PCAP with RTP protocol and look at payload type section :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*P_kJftCsiZY0465ezReSeg.png)

```
THE Answer : ITU-T G.711 PCMU
```

## **Q12-How long is the sampling time (in milliseconds)?**

Form first hint , i go to deepseek and search about the codec’s frequency:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*vZU0qmmS0wbA_BX2Vdxf9w.png)

Sample time = 1 / sample rate = 1/8000 = 0.125 ms

```
THE Answer : 0.125
```

## **Q13-What was the password for the account with username 555?**

i apply this filter in wireshark :

```
frame contains "username=555"
```

then in this screen :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*AA18uzqGp2c7kMlJ2v36Gw.png)

we found two packets , i choose first one and use Fint by “555” :

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*bRBNtxB80DA4Bmso3Sq_0A.png)

```
THE Answer : 1234
```

## **Q14-Which RTP packet header field can be used to reorder out of sync RTP packets in the correct sequence?**

filter the PCAP with RTP protocol and look at the details:

Press enter or click to view image in full size

![](https://miro.medium.com/v2/resize:fit:963/1*3fDw69qtUFnbGuK1JdiNZQ.png)

```
THE Answer : timestamp
```

## **Q15-The trace includes a secret hidden message. Can you hear it?**

filter the PCAP with RTP Protocol and go to

Telephony > RTP > RTP Player and click play , now listen to the message you will hear the answer :

```
THE Answer : MEXICO
```
