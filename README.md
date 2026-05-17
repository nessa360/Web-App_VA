# Web Application Vulnerability Assessment Report

**Assessor:** Vanessa Baah-Williams
**Target Application:** http://testasp.vulnweb.com
**Assessment Date:** 17 May 2026
**Tool Used:** OWASP ZAP (Zed Attack Proxy)
**Report Status:** Final

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Introduction](#2-introduction)
3. [Scope and Objectives](#3-scope-and-objectives)
4. [Methodology](#4-methodology)
5. [Summary of Findings](#5-summary-of-findings)
6. [Detailed Findings](#6-detailed-findings)
7. [Risk Matrix](#7-risk-matrix)
8. [Recommendations](#8-recommendations)
9. [Conclusion](#9-conclusion)
10. [References](#10-references)

---

## 1. Executive Summary

A web application vulnerability assessment was conducted against **testasp.vulnweb.com**, a deliberately vulnerable web application provided by Acunetix for legal security testing and educational purposes. The assessment used **OWASP ZAP**, an industry-standard open-source security testing tool, to identify weaknesses in the application.

A total of **19 vulnerabilities** were discovered across four severity levels:

| Severity | Count | Risk Level |
|----------|-------|------------|
| 🔴 High | 4 | Critical — requires immediate attention |
| 🟠 Medium | 4 | Significant — should be addressed soon |
| 🟡 Low | 7 | Minor — should be noted and monitored |
| 🔵 Informational | 4 | No direct risk — useful context |
| **Total** | **19** | |

The most critical findings include **SQL Injection**, **Path Traversal**, and **External Redirect** vulnerabilities, all of which could be exploited by an attacker to compromise the application and its underlying database. Immediate remediation of all high-severity issues is strongly recommended.

---

## 2. Introduction

### 2.1 What is a Web Application Vulnerability Assessment?

A web application vulnerability assessment is a structured security review process that identifies, classifies, and prioritizes security weaknesses in a web application. Unlike a penetration test, which actively exploits vulnerabilities, a vulnerability assessment focuses on **discovering and documenting** weaknesses so they can be fixed before a real attacker finds them.

### 2.2 Why is this important?

Web applications are one of the most common targets for cyberattacks. According to OWASP (Open Web Application Security Project), vulnerabilities like SQL Injection and Cross-Site Scripting (XSS) consistently rank among the most dangerous and most exploited security flaws worldwide. Identifying these weaknesses early helps organizations:

- Protect sensitive user data
- Prevent unauthorized access to systems
- Comply with data protection regulations (e.g. GDPR)
- Maintain user trust and application integrity

### 2.3 About the Target

**testasp.vulnweb.com** is a test web application intentionally built with security vulnerabilities by Acunetix, a cybersecurity company. It is provided specifically for security professionals, students, and researchers to practice vulnerability assessment legally and ethically. It simulates a real-world ASP-based web application with a database backend.

### 2.4 About OWASP ZAP

OWASP ZAP (Zed Attack Proxy) is a free, open-source web application security scanner maintained by the Open Web Application Security Project. It is one of the most widely used tools for finding vulnerabilities in web applications. ZAP works by:

- Acting as a **proxy** between the browser and the web application
- **Spidering** (crawling) the application to discover all pages and endpoints
- Running an **active scan** that probes each page for known vulnerabilities
- Generating a detailed **report** of all findings

---

## 3. Scope and Objectives

### 3.1 Scope

| Item | Details |
|------|---------|
| Target URL | http://testasp.vulnweb.com |
| Application Type | ASP-based web application with SQL database |
| Assessment Type | Automated scanning + manual review of findings |
| Tools Used | OWASP ZAP |
| Environment | Legal, sanctioned test environment |
| Out of Scope | Any other domain or IP address not listed above |

### 3.2 Objectives

The objectives of this assessment were to:

1. Identify all detectable security vulnerabilities in the target application
2. Classify each vulnerability by type and severity
3. Understand the potential impact of each vulnerability if exploited
4. Provide clear, actionable recommendations to fix each issue
5. Produce a professional report suitable for submission and review

### 3.3 Legal and Ethical Statement

This assessment was conducted **exclusively** on testasp.vulnweb.com, a legally sanctioned vulnerable application designed for security testing. No unauthorized systems were accessed. All testing was performed ethically and within the boundaries of the defined scope.

---

## 4. Methodology

The assessment followed a structured four-phase approach based on industry-standard practices:

### Phase 1 — Setup and Configuration
- Installed and configured OWASP ZAP on macOS
- Set the browser proxy to route traffic through ZAP (localhost:8080)
- Confirmed ZAP was capturing traffic from the target application
- Configured the target URL: http://testasp.vulnweb.com

### Phase 2 — Reconnaissance (Spidering)
- Used ZAP's **Traditional Spider** to crawl the entire application
- The spider followed all links, forms, and navigation paths to build a complete map of the application
- Used ZAP's **Ajax Spider** with Firefox to discover dynamically loaded content
- Result: A full sitemap of all pages and endpoints was generated

### Phase 3 — Active Scanning
- Launched ZAP's **Active Scan** against the full site map
- The active scan probed each discovered page and parameter for known vulnerability patterns including SQL Injection, XSS, Path Traversal, CSRF, and more
- The scan tested both GET and POST parameters
- Duration: Approximately 5–10 minutes
- Result: 19 alerts generated across 4 severity levels

### Phase 4 — Analysis and Reporting
- Reviewed each alert in ZAP's Alerts panel
- Categorized findings by severity (High, Medium, Low, Informational)
- Documented each vulnerability with description, impact, and recommendation
- Exported the full ZAP HTML report
- Captured screenshot evidence of findings

---

## 5. Summary of Findings

ZAP discovered **19 vulnerabilities** during the automated scan. The chart below summarizes findings by severity:

| # | Vulnerability | Severity | Instances |
|---|--------------|----------|-----------|
| 1 | SQL Injection | 🔴 High | 4 |
| 2 | SQL Injection – MsSQL Time Based | 🔴 High | 2 |
| 3 | External Redirect | 🔴 High | 2 |
| 4 | Path Traversal | 🔴 High | 2 |
| 5 | Absence of Anti-CSRF Tokens | 🟠 Medium | 4 |
| 6 | Content Security Policy (CSP) Header Not Set | 🟠 Medium | 1 |
| 7 | Application Error Disclosure | 🟠 Medium | 1 |
| 8 | Missing Anti-clickjacking Header | 🟠 Medium | 1 |
| 9 | HTTP Only Site | 🟡 Low | 1 |
| 10 | Cookie No HttpOnly Flag | 🟡 Low | 1 |
| 11 | Cookie without SameSite Attribute | 🟡 Low | 1 |
| 12 | Information Disclosure – Debug Error Messages | 🟡 Low | 1 |
| 13 | Server Leaks Info via X-Powered-By Header | 🟡 Low | 1 |
| 14 | Server Leaks Version via Server Header | 🟡 Low | 1 |
| 15 | X-Content-Type-Options Header Missing | 🟡 Low | 1 |
| 16 | GET for POST | 🔵 Info | 2 |
| 17 | Information Disclosure – Suspicious Comments | 🔵 Info | 1 |
| 18 | Session Management Response Identified | 🔵 Info | 1 |
| 19 | User Agent Fuzzer | 🔵 Info | 1 |

![ZAP Alerts Panel](screenshots/alerts.png)

---

## 6. Detailed Findings

---

### 6.1 SQL Injection
**Severity:** 🔴 High
**Instances Found:** 4
**OWASP Category:** A03:2021 – Injection

**What is it?**
SQL Injection occurs when an attacker inserts malicious SQL code into an input field (like a login form or search box). If the application does not properly validate or sanitize that input, the malicious code gets executed directly by the database. This is one of the most dangerous and oldest web vulnerabilities in existence.

**What did ZAP find?**
ZAP detected 4 endpoints in the application where user input is passed directly into SQL queries without proper sanitization. For example, entering `' OR '1'='1` into a login field could bypass authentication entirely.

**Potential Impact:**
- Complete bypass of login authentication
- Unauthorized access to the entire database
- Theft of usernames, passwords, and personal data
- Deletion or modification of database records
- In some cases, remote code execution on the server

**Recommendation:**
- Use **parameterized queries** (also called prepared statements) instead of building SQL queries by concatenating user input
- Implement an **ORM (Object Relational Mapper)** such as Entity Framework or Hibernate
- Validate and sanitize all user inputs before processing
- Apply the **principle of least privilege** to database accounts

---

### 6.2 SQL Injection – MsSQL Time Based
**Severity:** 🔴 High
**Instances Found:** 2
**OWASP Category:** A03:2021 – Injection

**What is it?**
This is a specific type of blind SQL injection where the attacker cannot see the database output directly. Instead, they inject SQL commands that cause the database to **pause (sleep) for a set number of seconds**. If the response is delayed, the attacker knows the injection worked. This technique is used to extract data one bit at a time without any visible output.

**What did ZAP find?**
ZAP detected 2 endpoints vulnerable to time-based SQL injection targeting Microsoft SQL Server. This confirms the backend uses **MsSQL** and that attackers could silently extract data from the database.

**Potential Impact:**
- Silent data exfiltration without leaving obvious traces
- Discovery of database structure, table names, and column names
- Extraction of sensitive user data over time

**Recommendation:**
- Same as 6.1 — use parameterized queries and input validation
- Monitor database query execution times for anomalies
- Implement a Web Application Firewall (WAF) to detect injection patterns

---

### 6.3 External Redirect
**Severity:** 🔴 High
**Instances Found:** 2
**OWASP Category:** A01:2021 – Broken Access Control

**What is it?**
An external redirect vulnerability occurs when a web application redirects users to a URL specified in a parameter, without validating whether that URL is safe or trusted. Attackers exploit this to send users from a trusted site to a malicious one.

**What did ZAP find?**
ZAP found 2 instances where the application accepts a URL as a parameter and redirects the user to it without any validation. For example: `http://testasp.vulnweb.com/redirect?url=http://malicious-site.com`

**Potential Impact:**
- **Phishing attacks** — users trust the original domain and click the link, ending up on a fake login page
- **Malware distribution** — users redirected to sites that install malware
- Damage to the organization's reputation

**Recommendation:**
- Never use user-supplied input directly in redirect URLs
- Maintain a **whitelist** of allowed redirect destinations
- If redirects are necessary, use indirect references (e.g. `?dest=1` mapped server-side to a known URL)

---

### 6.4 Path Traversal
**Severity:** 🔴 High
**Instances Found:** 2
**OWASP Category:** A01:2021 – Broken Access Control

**What is it?**
Path traversal (also called directory traversal) allows an attacker to access files and directories stored outside the intended web root folder. By manipulating file path parameters with sequences like `../../`, an attacker can navigate up the directory structure and read sensitive system files.

**What did ZAP find?**
ZAP detected 2 endpoints where file path parameters are not validated. An attacker could potentially access files like `/etc/passwd` (Linux) or `C:\Windows\System32\config\SAM` (Windows) by injecting traversal sequences.

**Potential Impact:**
- Access to sensitive configuration files
- Exposure of server credentials and API keys
- Reading application source code
- Full server compromise in severe cases

**Recommendation:**
- Validate and sanitize all file path inputs
- Use a **whitelist** of allowed file names/paths
- Run the web application with the minimum required file system permissions
- Use server-side path canonicalization to resolve and validate paths before use

---

### 6.5 Absence of Anti-CSRF Tokens
**Severity:** 🟠 Medium
**Instances Found:** 4
**OWASP Category:** A01:2021 – Broken Access Control

**What is it?**
Cross-Site Request Forgery (CSRF) is an attack where a malicious website tricks a logged-in user's browser into making unwanted requests to another site where the user is authenticated. Without CSRF tokens, the application cannot distinguish between legitimate requests from the user and forged ones from an attacker.

**What did ZAP find?**
4 forms in the application do not include CSRF tokens, meaning any form submission (like changing a password or making a transaction) could be triggered by a malicious third-party website without the user's knowledge.

**Potential Impact:**
- Unauthorized actions performed on behalf of authenticated users
- Password or email changes without user consent
- Financial transactions or data modifications

**Recommendation:**
- Implement **synchronizer token pattern** — include a unique, secret CSRF token in every form
- Use the **SameSite cookie attribute** to prevent cross-site cookie sending
- Validate the Origin and Referer headers on sensitive requests

---

### 6.6 Content Security Policy (CSP) Header Not Set
**Severity:** 🟠 Medium
**Instances Found:** 1
**OWASP Category:** A05:2021 – Security Misconfiguration

**What is it?**
A Content Security Policy is an HTTP response header that tells the browser which sources of content (scripts, styles, images) are trusted. Without it, the browser will execute any script it encounters, making XSS attacks far more effective.

**Potential Impact:**
- Increases the severity and exploitability of any XSS vulnerabilities present
- Allows malicious scripts from external sources to execute in users' browsers

**Recommendation:**
- Add a `Content-Security-Policy` HTTP header to all responses
- Start with a restrictive policy: `Content-Security-Policy: default-src 'self'`
- Gradually relax as needed for legitimate third-party resources

---

### 6.7 Application Error Disclosure
**Severity:** 🟠 Medium
**Instances Found:** 1

**What is it?**
The application displays detailed error messages to users when something goes wrong. These messages often contain sensitive information such as stack traces, database query details, server paths, and software versions — all useful to an attacker.

**Potential Impact:**
- Reveals internal application structure to attackers
- Exposes database schema details that aid SQL injection attacks
- Discloses server-side technology stack

**Recommendation:**
- Display generic, user-friendly error messages to end users
- Log detailed errors **server-side only**, never expose them in the browser
- Disable debug mode in production environments

---

### 6.8 Missing Anti-Clickjacking Header
**Severity:** 🟠 Medium
**Instances Found:** 1

**What is it?**
Clickjacking is an attack where a malicious page embeds the target application in a hidden iframe and tricks users into clicking on elements they cannot see. Without the X-Frame-Options or CSP frame-ancestors header, the application can be embedded by any website.

**Potential Impact:**
- Users unknowingly perform actions on the application (clicks, form submissions)
- Can be used to steal credentials or perform unauthorized transactions

**Recommendation:**
- Add the HTTP header: `X-Frame-Options: DENY` or `X-Frame-Options: SAMEORIGIN`
- Alternatively use CSP: `Content-Security-Policy: frame-ancestors 'none'`

---

### 6.9 Cookie Security Issues
**Severity:** 🟡 Low
**Findings:** Cookie No HttpOnly Flag | Cookie without SameSite Attribute

**What is it?**
Cookies that lack security attributes are vulnerable to theft and misuse:
- **HttpOnly flag missing** — JavaScript can access the cookie, enabling session theft via XSS
- **SameSite attribute missing** — cookies are sent with cross-site requests, enabling CSRF attacks

**Recommendation:**
- Set `HttpOnly` flag on all session cookies: `Set-Cookie: session=abc; HttpOnly`
- Set `SameSite=Strict` or `SameSite=Lax` on all cookies
- Set `Secure` flag to ensure cookies are only sent over HTTPS

---

### 6.10 Information Disclosure via HTTP Headers
**Severity:** 🟡 Low
**Findings:** X-Powered-By Header | Server Version Header | Debug Error Messages | X-Content-Type-Options Missing

**What is it?**
The server is leaking technical information through HTTP response headers, such as:
- The web framework being used (e.g. `X-Powered-By: ASP.NET`)
- The server software and version (e.g. `Server: Microsoft-IIS/7.5`)

This information helps attackers identify known vulnerabilities for that specific software version.

**Recommendation:**
- Remove or suppress `X-Powered-By` and `Server` headers in the web server configuration
- Add `X-Content-Type-Options: nosniff` to prevent MIME-type sniffing attacks
- Never expose version information in any HTTP response

---

### 6.11 Informational Findings
**Severity:** 🔵 Informational (no direct risk)

| Finding | Description |
|---------|-------------|
| GET for POST | Some POST endpoints also accept GET requests, which may expose sensitive data in URLs and server logs |
| Information Disclosure – Suspicious Comments | HTML source code contains developer comments that may reveal implementation details |
| Session Management Response Identified | ZAP detected session management mechanisms — useful for further manual testing |
| User Agent Fuzzer | ZAP tested different browser User-Agent strings — results suggest no major inconsistencies |

---

## 7. Risk Matrix

| Vulnerability | Likelihood | Impact | Overall Risk |
|--------------|------------|--------|--------------|
| SQL Injection | High | Critical | 🔴 Critical |
| MsSQL Time-Based SQLi | High | Critical | 🔴 Critical |
| External Redirect | Medium | High | 🔴 High |
| Path Traversal | Medium | High | 🔴 High |
| Absence of CSRF Tokens | Medium | Medium | 🟠 Medium |
| CSP Header Not Set | High | Medium | 🟠 Medium |
| Application Error Disclosure | High | Medium | 🟠 Medium |
| Missing Clickjacking Header | Low | Medium | 🟠 Medium |
| Cookie Security Issues | Medium | Low | 🟡 Low |
| Information Disclosure Headers | High | Low | 🟡 Low |

---

## 8. Recommendations

### Immediate Actions (High Priority)
1. **Fix SQL Injection** — Replace all dynamic SQL queries with parameterized queries or prepared statements. This is the single most important fix.
2. **Fix Path Traversal** — Validate and sanitize all file path inputs. Use server-side path whitelisting.
3. **Fix External Redirect** — Remove or restrict URL redirect parameters. Use a server-side whitelist of allowed destinations.

### Short-Term Actions (Medium Priority)
4. **Implement CSRF tokens** — Add unique tokens to all state-changing forms.
5. **Set security headers** — Add CSP, X-Frame-Options, and X-Content-Type-Options to all HTTP responses.
6. **Disable error disclosure** — Configure the application to show generic errors to users and log details server-side only.

### Ongoing Actions (Low Priority)
7. **Secure all cookies** — Add HttpOnly, SameSite, and Secure flags.
8. **Remove information-leaking headers** — Suppress X-Powered-By and Server version headers.
9. **Review HTML source** — Remove all developer comments from production code.
10. **Enable HTTPS** — Enforce HTTPS across the entire application.

---

## 9. Conclusion

This vulnerability assessment of **testasp.vulnweb.com** identified **19 security vulnerabilities**, including 4 of high severity. The application demonstrates several critical weaknesses commonly found in real-world web applications, particularly around input validation (SQL Injection, Path Traversal) and access control (External Redirect, CSRF).

The use of OWASP ZAP proved highly effective in automatically discovering a wide range of vulnerabilities in a short time. However, automated tools should always be complemented with manual testing to uncover logic flaws and context-specific vulnerabilities that scanners may miss.

Addressing the high-severity findings — especially SQL Injection — should be treated as an urgent priority, as these vulnerabilities could lead to complete application and database compromise if exploited by a malicious actor.

---

## 10. References

- [OWASP Top 10 (2021)](https://owasp.org/www-project-top-ten/)
- [OWASP ZAP Official Documentation](https://www.zaproxy.org/docs/)
- [OWASP SQL Injection Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)
- [OWASP CSRF Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross-Site_Request_Forgery_Prevention_Cheat_Sheet.html)
- [OWASP Clickjacking Defense Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Clickjacking_Defense_Cheat_Sheet.html)
- [Acunetix Test Applications](https://www.acunetix.com/blog/articles/acunetix-test-websites/)
- [NIST Web Application Security Guidelines](https://csrc.nist.gov/publications/detail/sp/800-95/final)

---

*This report was produced for educational purposes as part of a web application security assessment assignment. All testing was conducted on a legally sanctioned vulnerable application.*

*Assessor: Vanessa Baah-Williams | Date: 17 May 2026*