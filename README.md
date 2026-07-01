# elevate_lab_task2
# Cyber Security Internship - Task 2: Phishing Email Sample Analysis
## Project Overview
This project focuses on identifying indicators of compromise (IoCs) and social engineering traits in a suspicious email sample[span_0](start_span)[span_0](end_span). The analysis includes evaluating the sender's origin, assessing psychological triggers, and utilizing an online header analyzer to check technical security authentication[span_1](start_span)[span_1](end_span).
## Objective
To develop email threat analysis capabilities, recognize domain spoofing tactics, and analyze core technical indicators that distinguish malicious emails from authentic business communications[span_2](start_span)[span_2](end_span).
---
## 📊 Phishing Analysis Case Study Report
### 1. Phishing Sample Analyzed
- **Subject Line:** CRITICAL: Unauthorized login attempt blocked from Russia - Action Required!
- **Displayed Sender:** Google Accounts Security `<no-reply@secure-google-alert-login.com>`
- **Target Link Provided:** `http://myaccount.google.com.secure-google-alert-login.com/security/checkpoint`
### 2. Identified Phishing Indicators & Traits
- **Domain Spoofing (Typosquatting):** The email purports to originate from Google, but the domain registration address is `secure-google-alert-login.com`[span_3](start_span)[span_3](end_span). The structure is designed to look like an official alert domain to deceive users inspecting the sender field cursorily[span_4](start_span)[span_4](end_span).
- **Urgency and Coercion:** The text utilizes high-pressure call-to-action hooks ("instantly verify", "within 12 hours") and severe consequences ("permanently suspended") to manipulate the recipient into executing instructions without validation[span_5](start_span)[span_5](end_span).
- **Mismatched Hyperlink Architecture:** The target URL uses a subdomain layer string `myaccount.google.com` to project legitimacy. However, the true root domain is actually `secure-google-alert-login.com`, an unverified third-party destination controlled by the external attacker[span_6](start_span)[span_6](end_span).
- **Generic Personalization:** The communication lacks genuine subscriber contextual identification details, relying on a mass-distribution placeholder ("Dear User").
---
## 🛠️ Technical Header Analysis (Google Admin Toolbox Messageheader)
The raw email header was audited using the **Google Admin Toolbox Messageheader** utility[span_7](start_span)[span_7](end_span). The tool successfully parsed the routing metadata and flagged critical authentication failures[span_8](start_span)[span_8](end_span).
### Authentication Results Summary

| Security Protocol | Status | Details / Analysis |
| :--- | :--- | :--- |
| **SPF (Sender Policy Framework)** | 🔴 **fail** | Status marked as `fail with IP Unknown!`, showing the message did not originate from a designated server. |
| **DKIM (DomainKeys Identified Mail)** | 🔴 **fail** | Status marked as `fail with domain google.com;`, indicating cryptographic signature verification completely broke. |
| **DMARC (Domain-based Message Authentication)** | 🔴 **fail** | Alignment check completely failed because both SPF and DKIM validations were invalid. |

### Message Routing & Delivery Latency
According to the parsed hops in the header analyzer tool:
- **Origin to Gateway:** The message originated from `mail.secure-google-alert-login.com` and hit the Google gateway `mx.google.com` using the **ESMTPS** protocol with a delivery **delay of 12 seconds**.
- **Internal Hops:** Followed internal Google SMTP routing protocols between local node addresses (`2002:a17...` and `2002:a05...`) before reaching the destination mailbox tray.
---
## 🔒 Recommended Actions & Mitigation
1. **Immediate Deletion:** The email should be safely reported to the enterprise security team and permanently purged from the system[span_9](start_span)[span_9](end_span).
2. **Endpoint Block:** The malicious sender domain `secure-google-alert-login.com` should be blocked at the email gateway level.
3. **Local Security Controls:** Ensure network configurations remain completely isolated from public access profiles[span_10](start_span)[span_10](end_span).
