# 🖥️ Vectara - TryHackMe Write-Ups

This folder contains my write-ups from the **Vectara** cybersecurity challenges on TryHackMe.  
It demonstrates my learning in AI security, prompt injection, data poisoning, and agentic AI vulnerabilities.

---

## 📝 Challenges Solved

### 1. TRANSMISSION ZERO (Prompt Injection)
- **Difficulty:** Very Easy  
- **Flag:** Flag: TKM{REDACTED}

**Summary:** Exploited a direct prompt injection vulnerability by identifying the boundary between system instructions and user input to extract restricted internal data.

**Steps Taken:** 1. Analyzed AI response patterns to map out the system prompt logic.  
2. Crafted a role-play scenario to bypass guardrails.  
3. Successfully retrieved the hidden flag through direct conversation manipulation.

---

### 2. IN A PICKLE (AI Supply Chain Security)
- **Difficulty:** Very Easy  
- **Flag:** Flag: TKM{REDACTED}

**Summary:** Investigated vulnerabilities in the AI model storage infrastructure. Exploited an insecure S3-compatible bucket to access and manipulate model storage files.

**Steps Taken:** 1. Identified an exposed model storage bucket used to house sensitive model data.  
2. Navigated the bucket hierarchy to locate restricted files being used in the AI pipeline.  
3. Intercepted the flag by accessing the stored model metadata and configuration files.

---

### 3. GHOST SHIP (AI Supply Chain Security)
- **Difficulty:** Easy  
- **Flag:** Flag: TKM{REDACTED}

**Summary:** Analyzed the containerized supply chain of an AI agent, focusing on identifying leaked sensitive information within the environment variables and container manifests.

**Steps Taken:** 1. Audited the container environment and manifest files for leaked credentials and hardcoded secrets.  
2. Used the command line to inspect internal environment variables (env) used by the AI agent.  
3. Successfully recovered the flag hidden within the deployment's sensitive configuration metadata.

---

### 4. DEAD FREIGHT (Data Poisoning)
- **Difficulty:** Easy  
- **Flag:** Flag: TKM{REDACTED}

**Summary:** Executed a targeted data poisoning attack by injecting malicious samples into the training dataset used for model fine-tuning.

**Steps Taken:** 1. Located the dataset used for model training within the local filesystem.  
2. Injected "trigger" samples to force specific model biases during classification tasks.  
3. Verified the "drift" in the model's logic to confirm successful poisoning and reveal the flag.

---

### 5. GLITCHED TRANSIT (Data Poisoning)
- **Difficulty:** Easy  
- **Flag:** Flag: TKM{REDACTED}

**Summary:** Exploited a model's real-time learning mechanism by "glitching" the classification threshold through targeted input testing.

**Steps Taken:** 1. Identified the model's vulnerability where confidence scores were adjusted based on immediate user-provided feedback.  
2. Systematically tested boundary inputs to determine the exact point where the model's decision-making logic would fail.  
3. Successfully manipulated the classification probability until the transit gate glitched into an "Allow" state, revealing the flag.

---

### 6. GHOSTQUERY (Agentic AI)
- **Difficulty:** Easy  
- **Flag:** Flag: TKM{REDACTED}

**Summary:** Performed a Prompt-to-SQL injection attack by manipulating the natural language interface to execute unauthorized database queries.

**Steps Taken:** 1. Observed the agent's ability to interface with a SQL backend to search for user records.  
2. Crafted a natural language prompt containing SQL logical operators (e.g., `OR 1=1`) to break the intended query structure.  
3. Tricked the agent into dumping the entire database contents, including the administrative flag.

---

### 7. PROTOCOL DRIFT (Agentic AI)
- **Difficulty:** Easy  
- **Flag:** Flag: TKM{REDACTED}

**Summary:** A sophisticated attack combining Indirect Prompt Injection with Stored XSS to hijack an administrative bot's session and exfiltrate data.

**Steps Taken:** 1. Observed that the MedBoy assistant rendered notes as Rich HTML for the "Duty Pharmacist" review process.  
2. Filed a medical note containing a malicious `<img>` tag with an `onerror` JavaScript payload to capture session cookies.  
3. The automated reviewer executed the script upon viewing the note, sending the session data to a callback log where the flag was recovered.

---

## 🧠 Skills Practiced

- **Adversarial Prompting:** Bypassing LLM guardrails and system prompts.  
- **Infrastructure Auditing:** Exploiting insecure S3 buckets and container manifests.  
- **Data Integrity:** Manipulating training sets and feedback loops to influence model behavior.  
- **XSS in AI Context:** Delivering traditional web exploits via autonomous agents.

---

## 📂 Challenges Completed

- Prompt Injection & Jailbreaking  
- Supply Chain & Serialization Vulnerabilities  
- Training Data & Feedback Poisoning  
- Agentic AI Logic Exploitation

---

## 🔗 Related Work

- See [CTF Write-Ups Repository](https://github.com/chris12x1/CTF-Writeups) for all events.  
- See [DevSecCon25 Challenge Proof](https://github.com/chris12x1/devseccon25-proof) for additional cybersecurity projects.

---
**Note:** This lab focuses on the OWASP Top 10 for LLMs and demonstrates the intersection of AI logic and traditional web vulnerabilities.
