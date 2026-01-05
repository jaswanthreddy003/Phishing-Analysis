# Phishing Email – Header Analysis

## Overview

This section documents the **header-level investigation** of a phishing email impersonating **Chase Bank**.  
The objective of this analysis is to validate the sender’s authenticity, identify infrastructure abuse, and determine whether the email is malicious **without interacting with links or attachments**.

The email claims that the recipient’s bank account has been blocked due to unusual activity and urges immediate action.

---

## Sample Analyzed

- **Filename:** `sample1.eml`
- **Impersonated Brand:** Chase Bank
- **Analysis Scope:** Header analysis only

A rendered view of the phishing email (opened safely in an email client for visual reference) is included below:

![Phishing Email Screenshot](email_preview.png)

---

## Key Header Findings

- **From Address:** `alerts@chase.com` (brand impersonation)
- **Reply-To / Return-Path:** `@proton.me` (mismatch with claimed sender)
- **Sender IP:** `185.70.40.140`
- **Sending Infrastructure:** ProtonMail (Proton AG, Switzerland)
- **Message-ID Domain:** `@protonmail.com`

### Authentication Results

- **SPF:** Pass (for ProtonMail domain, not Chase)
- **DKIM:** Failed / Timeout
- **DMARC:** Pass (but aligned to ProtonMail, not Chase)

Despite some authentication checks passing, **domain alignment fails**, which is a strong indicator of phishing.

---

## IOC & Header Extraction Method

To automate extraction of indicators from the email header, the following command was used:

```bash
python3 eioc.py ../01_Header_Analysis/sample1.eml

