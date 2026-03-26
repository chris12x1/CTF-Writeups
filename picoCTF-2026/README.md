# 🖥️ picoCTF 2026 Write-Ups

This folder contains my write-ups from the **picoCTF 2026** cybersecurity challenges.  
It demonstrates my learning in Linux, Git, and privilege escalation, as well as problem-solving in CTF-style exercises.

---

## 📝 Challenges Solved

### 1. MY GIT
- **Difficulty:** Medium  
- **Points:** 50  
- **Flag:** `picoCTF{1mp3rs0n4t4_g17_345y_220a9833}`

**Summary:**  
This challenge required pushing a file to a Git repository hosted on a custom server. The goal was to update `flag.txt` using the correct credentials (`root:root@picoctf`).  

**Steps Taken:**  
1. Cloned the repository using the provided SSH command and password.  
2. Verified the folder contents (`flag.txt` present).  
3. Pushed the file using the correct root credentials.  
4. The flag was revealed upon successful push.

---

### 2. SUDO MAKE ME A SANDWICH
- **Difficulty:** Medium  
- **Points:** 50  
- **Flag:** `picoCTF{ju57_5ud0_17_9a782247}`

**Summary:**  
This challenge required reading a file (`flag.txt`) that had restricted permissions. Elevated privileges were necessary.  

**Steps Taken:**  
1. Connected to the challenge server via SSH using the provided credentials.  
2. Attempted to read `flag.txt` but got `Permission denied`.  
3. Ran `sudo -l` to check allowed sudo commands.  
4. Found that `/bin/emacs` could be run with sudo.  
5. Opened the file with `sudo emacs flag.txt` to read the flag.

---

## 🧠 Skills Practiced

- Linux commands & filesystem navigation  
- Git repository analysis & manipulation  
- Privilege escalation techniques  
- Analytical & logical thinking  

---

## 📂 Challenges Completed

- Beginner Linux challenges  
- Git manipulation exercises  
- Basic CTF problem-solving scenarios  

**Note:** No scripts or files were required for these exercises; the focus was on documenting solutions and understanding concepts.

---

## 🔗 Related Work

- See [CTF Write-Ups Repository](https://github.com/chris12x1/CTF-Writeups) for all events.  
- See [DevSecCon25 Challenge Proof](https://github.com/chris12x1/devseccon25-proof) for additional cybersecurity projects.

---

## 👤 Author

**Christopher Diaz**  
Cybersecurity Professional | CompTIA CySA+ | SIEM (Splunk) | Threat Detection | Incident Response
