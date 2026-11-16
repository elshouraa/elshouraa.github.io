---
title: Insider Lab by CyberDefenders
date: 2026-09-09 00:00:00 +0200
categories:
  - Write-ups
---

hi everyone, anther write-up for lab about my fav platform CyberDefenders

[Blue team CTF Challenges | insider — CyberDefenders](https://cyberdefenders.org/blueteam-ctf-challenges/insider/)

Category : Endpoint Forensics

![](https://cdn-images-1.medium.com/max/1361/1*FkOJl59Ks8D1CElI5XwtDw.png)

### Scenario :

After Karen started working for ‘TAAUSAI,’ she began doing illegal activities inside the company. ‘TAAUSAI’ hired you as a soc analyst to kick off an investigation on this case.

You acquired a disk image and found that Karen uses Linux OS on her machine. Analyze the disk image of Karen’s computer and answer the provided questions.

### **Q1: Which Linux distribution is being used on this machine?**

First of all, we will download FTK Imager from: [https://www.exterro.com/ftk-product-downloads/ftk-imager-4-7-3-81](https://www.exterro.com/ftk-product-downloads/ftk-imager-4-7-3-81) and import image file

go to **root → boot**

![Screenshot 2025-08-06 091804.png](/assets/img/posts/insider-lab-by-cyberdefenders/Screenshot_2025-08-06_091804.png)

```
kali
```

---

### **Q2: What is the MD5 hash of the Apache access.log file?**

go to root —> var —>log —> apache2

i found **access.log** file 

![Screenshot 2025-08-06 092314.png](/assets/img/posts/insider-lab-by-cyberdefenders/Screenshot_2025-08-06_092314.png)

then, i export it and calculate his **MD5 hash by PowerShell .**

![5.png](/assets/img/posts/insider-lab-by-cyberdefenders/5.png)

```jsx
d41d8cd98f00b204e9800998ecf8427e
```

---

### **Q3: It is suspected that a credential dumping tool was downloaded. What is the name of the downloaded file?**

> go to root →  root → Downloads→ apache2
> 

![4.png](/assets/img/posts/insider-lab-by-cyberdefenders/4.png)

```jsx
mimikatz_trunk.zip
```

---

### **Q4: A super-secret file was created. What is the absolute path to this file?**

> go to root →  root → .bash_history
> 

i found command that :

“touch snky snky > /root/Desktop/**SuperSecretFile.txt** ”

![image.png](/assets/img/posts/insider-lab-by-cyberdefenders/image.png)

```jsx
/root/Desktop/SuperSecretFile.txt
```

---

### **Q5: What program used the file didyouthinkwedmakeiteasy.jpg during its execution?**

> go to root → root → .bash_history
> 

i found this program “ binwalk ”

![Screenshot 2025-08-06 123102.png](/assets/img/posts/insider-lab-by-cyberdefenders/Screenshot_2025-08-06_123102.png)

```jsx
binwalk
```

---

### **Q6: What is the third goal from the checklist Karen created?**

go to **/root/Desktop/documents/checklist**

![8.png](/assets/img/posts/insider-lab-by-cyberdefenders/8.png)

```jsx
profit
```

---

### **Q7: How many times was Apache run?**

> go to root → var → log → apache2
> 

![](https://cdn-images-1.medium.com/max/1361/1*yA5fCD_oqB_sIDGAnXR3IQ.png)

now I don’t see any attempt to implement it.

```jsx
0
```

---

### **Q8:This machine was used to launch an attack on another. Which file contains the evidence for this?**

> go to root → root → irZLAohL.jpeg
> 

![10.png](/assets/img/posts/insider-lab-by-cyberdefenders/10.png)

```jsx
irZLAohL.jpeg
```

---

### **Q9:It is believed that Karen was taunting a fellow computer expert through a bash script within the Documents directory. Who was the expert that Karen was taunting?**

> go to root → root → documents → myfristhack —> fristscript_fixed
> 

![11.png](/assets/img/posts/insider-lab-by-cyberdefenders/11.png)

```jsx
Young
```

---

### **Q10:A user executed the su command to gain root access multiple times at 11:26. Who was the user?**

> go to root → var → log → auth.log
> 

postgres execute the su command to gain root access multiple times

![12.png](/assets/img/posts/insider-lab-by-cyberdefenders/12.png)

```jsx
postgres
```

---

### **Q11:Based on the bash history, what is the current working directory?**

Based on the bash history,

> go to root → root →.bash_history
> 

![1_WEUXtqy1zD8buRSnIrkgvA.png](/assets/img/posts/insider-lab-by-cyberdefenders/1_WEUXtqy1zD8buRSnIrkgvA.png)

![Screenshot 2025-08-06 123149.png](/assets/img/posts/insider-lab-by-cyberdefenders/Screenshot_2025-08-06_123149.png)

```
/root/Documents/myfirsthack/
```

# **Thanks For Reading**

#CyberDefenders #CyberSecurity #BlueYard #BlueTeam #InfoSec #SOC #SOCAnalyst #DFIR #CCD #CyberDefender
