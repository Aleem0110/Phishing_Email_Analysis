# 🕵️‍♂️ Phishing Email Header Analysis — Hobatere Lodge Namibia

This project documents the forensic analysis of a suspicious email marked as spam, allegedly from "Hobatere Lodge Namibia". The investigation includes header authentication, relay tracing, and phishing indicators.

---

## 📌 Email Summary

- **Subject:** Please confirm your account  
- **Sender:** hobatere.asylum.com.ua  
- **Language:** Mixed (Russian + English)  
- **Spam Reason:** Previous messages from domain marked as spam  
- **Suspicious Link:** `http://mcm1.com.ph/index.php?id=29115`  
- **Visual Bait:** Legitimate-looking "Confirm Account" button

---

## 🚨 Phishing Indicators

- **Domain Mismatch:** `hobatere.asylum.com.ua` ≠ `hobatere.com.na`  
- **Language Confusion:** Russian salary message + English lodge branding  
- **Link Destination:** `.com.ph` domain — unrelated to Namibia  
- **DKIM Authentication Failed**  
- **DMARC Non-Compliant**  
- **SPF Passed via Amazon SES**  
- **Spam History Flagged by Gmail**

> 🧠 These indicators confirm a phishing attempt using brand impersonation and spoofed headers.

---

## 📡 SMTP Relay Path Breakdown

| Hop | Delay     | From                          | By                     | With  | Time (UTC)           |
|-----|-----------|-------------------------------|------------------------|-------|----------------------|
| 1   | 0s        | hubble-noreply@google.com     | mx.google.com          | SMTP  | 10/25/23 18:41:24    |
| 2   | 0s        | mx.google.com                 | us-east-2.amazonses.com| SMTP  | 10/25/23 18:41:24    |
| 3   | 1s        | us-east-2.amazonses.com       | smtp.gmail.com         | SMTP  | 10/25/23 18:41:25    |

> 🔍 Amazon SES relay used — common in spoofed campaigns. No delay suggests automated delivery.

---

## 🔐 Authentication Protocols

### ✅ SPF (Sender Policy Framework)
- **Status:** Pass  
- **Details:** Amazon SES authorized for domain  
- **Note:** SPF alone doesn't verify sender identity

### ❌ DKIM (DomainKeys Identified Mail)
- **Status:** Fail  
- **Details:** Signature missing or invalid  
- **Impact:** Message integrity cannot be verified

### ❌ DMARC (Domain-based Message Authentication)
- **Status:** Non-Compliant  
- **Details:** DKIM failed → DMARC failed  
- **Impact:** Sender not authorized by domain policy

---

## 🧠 Forensic Verdict

> This email is a **phishing attempt** using brand impersonation, spoofed headers, and deceptive content.  
> Authentication failures and domain mismatch confirm **unauthenticated origin**.  
> The embedded link is likely malicious and unrelated to the claimed sender.

---

## 🛡️ Recommended Actions

- Block domain: `asylum.com.ua`  
- Report to: [PhishTank](https://www.phishtank.com/)  
- Educate users on mixed-language phishing tactics  
- Monitor Amazon SES relays for abuse

---

## 📚 Tools Used

- [MXToolbox Email Header Analyzer](https://mxtoolbox.com/EmailHeaders.aspx)  
- Gmail “Show Original” feature  
- GitHub for documentation  
- Screenshots from email and header analysis tools

---

## 🧠 Author

**Mohammed Aleem Hasan**  
Cybersecurity Enthusiast | Networking & IT infrastructure Learner.
