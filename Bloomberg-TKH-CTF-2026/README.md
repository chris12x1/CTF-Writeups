# 🏆 Bloomberg × The Knowledge House CTF 2026 — Write-Up

**Team:** `Ctrl_Alt_Defeat` &nbsp;|&nbsp; **Result:** 🥇 **1st Place** &nbsp;|&nbsp; **Progress:** 27/27 levels (−1 → 25, including the hidden secret level)

A hands-on, web-focused Capture The Flag built by **Bloomberg's Product Security team** for The Knowledge House's annual Hackathon. The challenge ran across a live target and progressed from basic source-code recon to chained authentication bypasses, with each level mapping to a real-world vulnerability class.

> ⚠️ **Authorization & Ethics:** All testing was performed against a sanctioned CTF platform during an organized, time-boxed event with explicit permission. These write-ups are for educational purposes only. The same techniques used here are used by penetration testers and security researchers under authorization — never against systems you do not own or have written permission to test.

> 🔒 **Note on paths:** Environment-specific next-level URL hashes are abbreviated or omitted. The focus is on **methodology and root cause**, not raw answer keys.

---

## 🧭 Summary

| Level | Category | Technique | Flag / Result |
|------:|----------|-----------|---------------|
| −1 | Information Disclosure | Hidden HTML comment in source | Path → `REDACTED` |
| 0 | Forced Browsing | Sequential URL tampering | Path → `REDACTED` |
| 1 | Broken Authentication | Default credentials (`REDACTED`) | Auto-advanced |
| 2 | Sensitive Data Exposure | Leaked custom HTTP response header | Next-level path leaked |
| 3 | Client-Side Secrets | `REDACTED` via `REDACTED` Base64 | Decoded path |
| 4 | Parameter Tampering | Hidden field `REDACTED` → `REDACTED` | Bypassed EULA gate |
| 5 | Insecure Session Mgmt | Forged cookie `REDACTED` | Bypassed auth |
| 6 | Broken JWT Validation | Flipped `REDACTED`, unverified signature | Privilege escalation |
| 7 | Access Control Bypass | `REDACTED` spoof | Localhost gate bypassed |
| 8 | Hardcoded Credentials | `REDACTED` on ELF binary | `REDACTED` |
| 9 | Insecure Client Crypto | SHA-256 hash cracked (CrackStation) | `REDACTED` |
| 10 | Open Redirect | Schemaless/mixed-slash bypass `REDACTED` | External redirect forced |
| 11 | Verbose Error / HPP | HTTP Parameter Pollution `REDACTED` | EJS stack trace leak |
| 12 | Client Crypto / Obfuscation | CryptoJS AES decrypt w/ recovered passphrase | Decoded path |
| 13 | Hidden Asset Disclosure | Unlinked PNG via Network tab | `REDACTED` |
| 14 | Prompt Injection | "Ignore previous instructions" override | Leaked next-level path |
| 15 | SQL Injection | Auth bypass `REDACTED` | Logged in w/o password |
| 16 | Command Injection | `REDACTED` → `REDACTED` | RCE on host |
| 17 | Network Fundamentals | `REDACTED` subnet math | net `REDACTED` / bcast `REDACTED` / 30 hosts |
| 18 | Code Analysis | Reconstruct Python socket scanner | `REDACTED` |
| 19 | Reverse Engineering | Deobfuscate JS C2 beacon | `REDACTED` |
| 20 | Predictable Tokens | MD5 of sequential integer | `REDACTED` |
| 21 | Path Traversal | Non-recursive filter bypass `REDACTED` | `REDACTED` |
| 22 | Business Logic | Negative-value credit transfer (`REDACTED`) | Balance inflated |
| 23 | Chained Exploit | Leaked JWT secret + forged token + IP spoof | Vault breached |
| 24 | Hidden Content | Decoy "complete" page + hidden DOM link | Found secret level |
| 25 | Meta Challenge | "Information hidden in plain sight" | 🎯 Master of Security |

---

## 📂 Detailed Write-Ups

### Level −1 — Information Disclosure (Source Code Comments)
**Objective:** Find the hidden entry point from a landing page with no visible navigation.
**Technique:** Manual source-code review (View Source) revealed a developer HTML comment documenting the first challenge route.
**Lesson:** Comments ship to the client. Routing details and architectural notes leaked in source are reconnaissance gold.

### Level 0 — Forced Browsing / Predictable Resource Location
**Objective:** Advance from the Level 0 intro screen with no redirect button.
**Technique:** Anticipated sequential routing and manually edited the URL `REDACTED`.
**Lesson:** Sequential, guessable resource paths with no authorization check let users navigate directly to protected resources.

### Level 1 — Broken Authentication (Default Credentials)
**Technique:** Submitted classic defaults `REDACTED` / `REDACTED`.
**Lesson:** Default and easily brute-forced credentials remain a persistent OWASP Top 10 issue.

### Level 2 — Sensitive Data Exposure (HTTP Headers)
**Technique:** DevTools → Network → inspected the document request's **Response Headers**; the next-level path was leaked in a custom server header (`REDACTED`).
**Lesson:** Custom headers are visible to anyone with DevTools. Never leak routing or version data there.

### Level 3 — Client-Side Secrets Exposure
**Technique:** A `REDACTED` block set `REDACTED`. Decoded the Base64 to recover the path.
```js
REDACTED
```
**Lesson:** Base64 is encoding, not encryption. Secrets must never live client-side.

### Level 4 — Client-Side Parameter Tampering
**Technique:** Located a hidden input and flipped its value in the DOM before submitting.
```html
REDACTED
```
**Lesson:** Business-logic state (EULA acceptance, privilege flags) must be validated server-side, never trusted from client inputs.

### Level 5 — Insecure Session Management
**Technique:** Set the required session cookie via the Console and reloaded.
```js
REDACTED
```
**Lesson:** Client-modifiable cookies must not drive privilege decisions unless cryptographically signed (and flagged `REDACTED` / `REDACTED`).

### Level 6 — Broken JWT Validation
**Technique:** Decoded the JWT payload, flipped the admin claim, and reassembled the token with the **original (unvalidated) signature**.
```json
REDACTED
```
**Lesson:** Servers must verify the JWT signature against a server-side secret before trusting any claim.

### Level 7 — Access Control Bypass via Spoofed Header
**Technique:** The route only served the flag to `REDACTED`. Spoofed the origin with a forged proxy header via `REDACTED`.
```bash
REDACTED
```
**Lesson:** `REDACTED` is user-controllable. Never use it for security boundaries unless a trusted upstream proxy overwrites it.

### Level 8 — Use of Hardcoded Credentials (Static Analysis)
**Technique:** Ran `REDACTED` against the provided 64-bit ELF binary; the password sat in cleartext next to usage strings.
```bash
REDACTED
```
**Lesson:** Secrets baked into binaries are trivially recovered with basic static analysis (CWE-259).

### Level 9 — Insecure Client-Side Cryptographic Verification
**Technique:** Found a client-side `REDACTED` comparing input to a hardcoded **SHA-256** digest (`REDACTED`). Reversed it via offline lookup (CrackStation).
```
REDACTED
```
**Lesson:** Authentication logic and secret comparison belong server-side. Unsalted hashes of common words fall instantly to rainbow tables.

### Level 10 — Open Redirect
**Technique:** The redirect filter only checked for a leading `REDACTED`. Used a mixed-slash payload so the browser normalized it into an absolute host.
```
REDACTED
```
**Lesson:** Validate redirects against an allowlist of target pages — not naive string-prefix checks.

### Level 11 — Verbose Error / HTTP Parameter Pollution
**Technique:** Passed a query param as an array to break the template engine's string assumptions, triggering a verbose stack trace.
```
REDACTED
```
The `REDACTED` engine panicked, leaking internal server paths (`REDACTED`) and the next-level route.
**Lesson:** Unhandled exceptions disclose internal structure. Catch errors and return generic messages in production.

### Level 12 — Client-Side Crypto / Obfuscation
**Technique:** Source held a CryptoJS AES blob (`REDACTED`) and an obfuscated key array. Dumped the array in DevTools, recovered the passphrase (`REDACTED`), and decrypted client-side.
```js
REDACTED
```
**Lesson:** If the key is in the client, the "encryption" is decorative. Obfuscation ≠ security.

### Level 13 — Hidden Asset Disclosure
**Technique:** An image was fetched but never rendered. Caught it in the **Network** tab by its PNG magic bytes (`REDACTED`) and viewed the **Preview** → flag rendered on the image.
**Result:** `REDACTED`
**Lesson:** Assets requested but hidden from the DOM are still fully accessible via network inspection.

### Level 14 — Prompt Injection
**Technique:** Sent an adversarial override to a guardrailed chatbot to make it surface protected data.
```
REDACTED
```
The bot's input validation failed and leaked the next-level path in an alert.
**Lesson:** LLM guardrails must be enforced outside the prompt; untrusted input should never reach instruction context unsanitized.

### Level 15 — SQL Injection (Auth Bypass)
**Technique:** Injected a tautology into the username field to force a universally-true `REDACTED` clause.
```sql
REDACTED
```
**Lesson:** Use parameterized queries / prepared statements. Never concatenate user input into SQL.

### Level 16 — Command Injection
**Technique:** A "Check User" lookup passed input into a shell. Chained a command with `REDACTED`.
```
REDACTED
```
**Lesson:** Never pass user input to a shell. Use safe APIs and strict allowlists; running as `REDACTED` still enables real damage.

### Level 17 — Network Fundamentals (Subnetting)
**Technique:** Given Host `REDACTED`, Gateway `REDACTED`, prefix `REDACTED`. Block size = REDACTED.
- Network: REDACTED`
- Broadcast: `REDACTED`
- Usable hosts: REDACTED (minus network + broadcast)

**Lesson:** Core IR/triage skill — knowing your subnet boundaries scopes an incident fast.

### Level 18 — Code Analysis (Socket Scanner Reconstruction)
**Technique:** Reconstructed a partial Python port scanner from fragments + stdout. Matched `REDACTED` to the built-in `REDACTED` module; logs showed open ports 22 and 443.
```
REDACTED
```
**Lesson:** Reading runtime output and matching it to language primitives is everyday reverse-engineering.

### Level 19 — Reverse Engineering (Deobfuscation)
**Technique:** Reconstructed an obfuscated JS C2 beacon string from three encodings.
```js
REDACTED
```
**Result:** `REDACTED`
**Lesson:** Layered string obfuscation is reversible by peeling encodings one at a time.

### Level 20 — Predictable Tokens / Weak Hashing
**Technique:** Tokens were `REDACTED`, `REDACTED`, `REDACTED`… Predicted slot REDACTED as `REDACTED`.
```
REDACTED
```
**Lesson:** Tokens must be unpredictable (CSPRNG). MD5 of sequential integers is trivially forgeable.

### Level 21 — Path Traversal (Non-Recursive Filter Bypass)
**Technique:** The filter stripped `REDACTED` in a single pass. A nested payload survived because removing the inner `REDACTED` collapsed into a valid one.
```
REDACTED
```
**Result:** `REDACTED`
**Lesson:** Sanitize recursively (or canonicalize + allowlist). Single-pass string replacement is bypassable.

### Level 22 — Business Logic (Negative-Value Abuse)
**Technique:** The credit-transfer field didn't reject negatives. Transferring `REDACTED` subtracted a negative → addition.
```
REDACTED
```
**Lesson:** Validate ranges and signs server-side; model financial logic against adversarial inputs.

### Level 23 — Chained Exploit (Info Disclosure → Auth Forgery → ACL Bypass)
**Technique:** No single bypass worked; chained three:
1. **Disclosure:** `REDACTED` leaked a migrated endpoint `REDACTED`; calling it with `REDACTED` returned the **HS256 signing material**.
2. **Forgery:** Forged an admin JWT signed with the recovered secret (Python `REDACTED`/`REDACTED`).
3. **ACL bypass:** Added `REDACTED` to satisfy the internal-origin check.
```json
REDACTED
```
**Result:** `REDACTED` — vault breached.
**Lesson:** Real attacks chain low-severity findings. An info leak + a trust flaw compound into full compromise.

### Level 24 — Hidden Content (Decoy Page)
**Technique:** The "🎉 Congratulations, you've completed the CTF!" page was a decoy. Inspecting the DOM (and the console hint `REDACTED`) exposed a hidden link to the secret level.
**Lesson:** Trust the source tree, not the rendered view. "The end" is sometimes hidden in plain sight.

### Level 25 — 🎯 The Meta Challenge (Secret Level)
Reaching the hidden final level confirmed full completion. The meta-lesson tied the whole CTF together: **information can be hidden in plain sight** — always check the source, the comments, the network, and the DOM.
**Final Achievement:** *Master of Security.*

---

## 🛠️ Tools & Techniques Used
- **Browser DevTools** — Elements/DOM, Console, Network, Application (cookies/storage)
- **`curl`** — custom headers & request crafting
- **CyberChef** — Base64/JWT decode/encode, hashing
- **CrackStation** — offline hash lookup (SHA-256, MD5)
- **`strings`** — ELF static analysis (WSL2 Ubuntu)
- **Python** — `hmac` / `hashlib` for HS256 JWT forgery; `socket` analysis
- **CryptoJS** — client-side AES/SHA inspection

## 🧠 Vulnerability Classes Covered
Information disclosure · broken authentication · session management · JWT/authorization flaws · SQL injection · command injection · prompt injection · path traversal · open redirect · client-side cryptography · reverse engineering · business-logic abuse · exploit chaining · network fundamentals.

## ✍️ Key Takeaways
- **Never trust the client.** Cookies, hidden fields, JWTs, headers, and JS are all user-controllable.
- **Encoding ≠ encryption.** Base64 and obfuscation only slow an attacker down.
- **Errors leak.** Verbose stack traces and headers are reconnaissance.
- **Chains beat singles.** The hardest level fell only by combining three "minor" flaws.
- **Read the source.** From Level −1 to the secret level, the answer was often hidden in plain sight.

---

*Write-up by Christopher Diaz ([@chris12x1](https://github.com/chris12x1)) — Team `Ctrl_Alt_Defeat`, 🥇 1st Place, Bloomberg × The Knowledge House CTF 2026.*

