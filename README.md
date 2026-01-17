# sidefx-privacy-bug
Security case study: SideFX user profile privacy control failure (Error S04-87, CWE-863)
# SideFX User Profile Privacy Control Failure – Security Case Study

## 📌 Overview
This repository documents a responsibly disclosed **functional privacy control vulnerability** in the SideFX user profile system.  
The bug prevents users from making their profiles private, forcing all profiles to remain publicly accessible.

**Key Points:**
- Vulnerability: Privacy control fails to save (**Error S04-87**)  
- Affected: All users (including legacy staff accounts)  
- Classification: CWE-863 (Incorrect Authorization)  
- Severity: High (CVSS 3.1: 7.5)  

> All sensitive PII and private URLs have been **redacted** to ensure responsible disclosure.

---

## 🛑 Vulnerability Summary
SideFX offers a privacy setting to hide user profiles from unregistered visitors.  
However, attempting to change this setting:

- Returns **Error S04-87**  
- Fails to save user preference  
- Forces profile to remain **publicly visible**  

This is fully reproducible and affects all users.

---

## 🔍 Steps to Reproduce

**1. Privacy Control Failure**  
1. Login to SideFX account  
2. Navigate: `Profile → Personal Info → Privacy`  
3. Uncheck “Make my user profile visible to unregistered visitors?”  
4. Click `Save changes`  

**Expected Result:**  
- Checkbox remains unchecked  
- Profile hidden from unauthenticated users  
- Success message displayed  

**Actual Result (Bug):**  
- Error: `"There was an error processing your request. [CODE: S04-87]"`  
- Setting does not save  
- Page refresh → checkbox checked again  
- Profile remains public  

**2. Verification Without Authentication**  
- Logout completely  
- Open private/incognito browser  
- Navigate to any user profile → fully visible  

---

## ⚠️ Security Impact

- **User Privacy Exposure:** All profiles remain public, including legacy staff accounts.  
- **Functional Vulnerability:** Privacy feature advertised but fails to enforce settings.  
- **Industry Implications:** Highlights the importance of **functional privacy controls** and secure defaults.

---

## 🔄 Recommended Fix

- Debug and resolve **Error S04-87** in the privacy module  
- Ensure `Save` operation commits privacy preference correctly  
- Add automated tests to validate privacy toggle works for all users  
- Implement server-side enforcement of privacy settings  

---

## 🛡️ Best Practices

- Do not rely solely on frontend checks for privacy controls  
- Always test save functionality, especially for legacy accounts  
- Monitor production systems for unintentional exposure of PII  
- Document reproducible PoCs for responsible disclosure  

---

## 📅 Disclosure Timeline

- **Dec 8, 2025:** Initial report submitted  
- **Dec 10, 2025:** Report closed as Duplicate (original report private)  
- **Dec 13, 2025:** Disclosure request submitted  
- **Dec 16, 2025:** Disclosure request withdrawn  
- **Dec 22, 2025:** Follow-up appeal sent for classification clarification  
- **Jan 1, 2026:** Disclosure request re-submitted  

> Full evidence (video, HTTP logs, screenshots) retained internally for portfolio purposes.

---

## 📚 References

- CWE-863: Incorrect Authorization  
- CWE-1188: Insecure Default Initialization  
- CVSS v3.1 Calculator – High severity  

---

## ⚖️ Disclaimer

This write-up is for **educational, portfolio, and responsible disclosure purposes only**.  
No live systems, PII, or unauthorized data has been exposed publicly.
