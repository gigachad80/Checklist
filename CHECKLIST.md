## 📋 Table of Contents

* [🎯 Pre-Hunt Preparation](#-pre-hunt-preparation)
* [🔍 Phase 1: Reconnaissance & Information Gathering](#-phase-1-reconnaissance--information-gathering)
* [🔧 Phase 2: Configuration & Infrastructure Testing](#-phase-2-configuration--infrastructure-testing)
* [🔐 Phase 3: Authentication & Session Management](#-phase-3-authentication--session-management)
* [🛡️ Phase 4: Authorization & Access Control](#️-phase-4-authorization--access-control)
* [💉 Phase 5: Input Validation & Injection Attacks](#-phase-5-input-validation--injection-attacks)
* [🌐 Phase 6: Client-Side Security](#-phase-6-client-side-security)
* [📱 Phase 7: Modern Web Application Security](#-phase-7-modern-web-application-security)
* [🔒 Phase 8: Business Logic & Application-Specific Testing](#-phase-8-business-logic--application-specific-testing)
* [🔐 Phase 9: Cryptography & Data Protection](#-phase-9-cryptography--data-protection)
* [📤 Phase 10: File Upload & Processing](#-phase-10-file-upload--processing)
* [💳 Phase 10.5: Payment & Card Processing Security](#-phase-105-payment--card-processing-security)
* [🚫 Phase 11: Denial of Service Testing](#-phase-11-denial-of-service-testing)
* [🔍 Phase 12: Advanced Attack Techniques](#-phase-12-advanced-attack-techniques)
* [📝 Phase 13: Documentation & Reporting](#-phase-13-documentation--reporting)
* [🛠️ Tools & Resources](#️-tools--resources)
* [⚠️ Important Notes](#️-important-notes)

---

## 🎯 Pre-Hunt Preparation

### Target Selection & Scope Definition
- [ ] Choose target based on program reputation and payout structure
- [ ] Read program policy thoroughly (scope, out-of-scope items, rules)
- [ ] Understand accepted vulnerability types
- [ ] Check for duplicate submission policies
- [ ] Note any specific testing restrictions
- [ ] Set up dedicated testing environment/VM
- [ ] Prepare necessary tools and proxies
- [ ] Document target's main domains and subdomains

## 🔍 Phase 1: Reconnaissance & Information Gathering

### 1.1 Passive Reconnaissance
- [ ] **Wildcard Domain Reconnaissance**
  - [ ] Run Amass for comprehensive subdomain enumeration
  - [ ] Use Subfinder for fast subdomain discovery
  - [ ] Execute Assetfinder for additional subdomain sources
  - [ ] Run DNSGen for subdomain permutation generation
  - [ ] Use MassDNS for bulk DNS resolution
  - [ ] Apply HTTProbe to check for live hosts
  - [ ] Run Aquatone for visual screenshots of alive hosts

- [ ] **Single Domain Scanning**
  - [ ] Comprehensive Nmap scan with service detection
  - [ ] Burp Suite crawler for comprehensive mapping
  - [ ] FFUF for directory and file fuzzing
  - [ ] Hakrawler/GAU/ParamSpider for URL discovery
  - [ ] LinkFinder for endpoint discovery in JavaScript
  - [ ] Extract URLs from Android applications (if applicable)

- [ ] **Manual Intelligence Gathering**
  - [ ] Shodan reconnaissance for exposed services
  - [ ] Censys search for certificates and services
  - [ ] Google dorking for exposed files/directories
  - [ ] Pastebin searches for leaked credentials
  - [ ] GitHub/GitLab code search for secrets and endpoints
  - [ ] OSINT gathering from multiple sources

- [ ] **Domain Enumeration**
  - [ ] Subdomain discovery using multiple sources (crt.sh, Subfinder, Amass)
  - [ ] Check DNS records (A, AAAA, CNAME, MX, TXT, NS)
  - [ ] Reverse DNS lookups
  - [ ] ASN enumeration for related IP ranges
  - [ ] Check for wildcard subdomains

- [ ] **Search Engine Intelligence**
  - [ ] Google dorking for exposed files/directories
  - [ ] Bing, DuckDuckGo, Yandex searches
  - [ ] Check archive.org for historical data
  - [ ] GitHub/GitLab code search for secrets
  - [ ] Shodan/Censys for exposed services

- [ ] **Social Media & Public Information**
  - [ ] LinkedIn employee enumeration
  - [ ] Twitter/social media mentions
  - [ ] Job postings for technology stack info
  - [ ] Company blog posts and documentation
  - [ ] Public presentations and conferences

### 1.2 Active Reconnaissance
- [ ] **Port Scanning & Service Detection**
  - [ ] Nmap comprehensive scan (-sS, -sV, -sC, -A)
  - [ ] UDP port scanning for common services
  - [ ] Service version identification
  - [ ] Default credential testing

- [ ] **Web Application Discovery**
  - [ ] Directory/file brute forcing (Gobuster, Dirb, Dirsearch)
  - [ ] Technology stack identification (Wappalyzer, BuiltWith)
  - [ ] CMS detection and version identification
  - [ ] Check for common files (robots.txt, sitemap.xml, .well-known/)
  - [ ] Backup file discovery (.bak, .old, .tmp, ~)

### 1.3 Application Mapping
- [ ] **Manual Exploration**
  - [ ] Browse entire application manually
  - [ ] Map all functionality and user roles
  - [ ] Identify all entry points and parameters
  - [ ] Note file upload functionalities
  - [ ] Document API endpoints
  - [ ] Identify client-side code and technologies
  - [ ] Check for multiple versions/channels (web, mobile web, mobile app, web services)
  - [ ] Identify co-hosted and related applications
  - [ ] Document all hostnames and ports
  - [ ] Identify third-party hosted content
  - [ ] Look for debug parameters

- [ ] **Automated Spidering**
  - [ ] Burp Suite spider/crawler
  - [ ] OWASP ZAP automated scan
  - [ ] Custom crawler scripts
  - [ ] JavaScript analysis for hidden endpoints

- [ ] **Content Discovery**
  - [ ] Check for files that expose content (robots.txt, sitemap.xml, .DS_Store)
  - [ ] Check caches of major search engines for publicly accessible sites
  - [ ] Test for differences in content based on User Agent (Mobile sites, search engine crawler access)
  - [ ] Perform comprehensive web application fingerprinting

## 🔧 Phase 2: Configuration & Infrastructure Testing

### 2.1 Server Configuration
- [ ] **HTTP Security Headers**
  - [ ] X-Frame-Options (Clickjacking protection)
  - [ ] X-XSS-Protection
  - [ ] X-Content-Type-Options
  - [ ] Content-Security-Policy (CSP)
  - [ ] Strict-Transport-Security (HSTS)
  - [ ] Referrer-Policy
  - [ ] Permissions-Policy/Feature-Policy

- [ ] **SSL/TLS Configuration**
  - [ ] SSL certificate validation (Duration, Signature, CN)
  - [ ] SSL version and algorithm strength
  - [ ] Key length verification
  - [ ] Protocol version support
  - [ ] Certificate transparency logs
  - [ ] Mixed content issues
  - [ ] SSL pinning bypass
  - [ ] Verify credentials only delivered over HTTPS
  - [ ] Ensure login forms delivered over HTTPS
  - [ ] Confirm session tokens only delivered over HTTPS
  - [ ] Verify HSTS implementation

- [ ] **Server Information Disclosure**
  - [ ] Server version in headers
  - [ ] Technology stack fingerprinting
  - [ ] Error message information disclosure
  - [ ] Debug information exposure
  - [ ] Source code comments
  - [ ] Check for sensitive data in client-side code (API keys, credentials)

- [ ] **HTTP Methods & Configuration**
  - [ ] Check HTTP methods supported and Cross Site Tracing (XST)
  - [ ] Test file extensions handling
  - [ ] Test for policies (Flash, Silverlight, robots)
  - [ ] Test for non-production data in live environment

### 2.2 Access Controls & Permissions
- [ ] **File & Directory Permissions**
  - [ ] Sensitive file exposure
  - [ ] Directory listing enabled
  - [ ] Backup file accessibility
  - [ ] Configuration file exposure
  - [ ] Log file accessibility
  - [ ] Check for commonly used application and administrative URLs
  - [ ] Check for old, backup and unreferenced files

## 🔐 Phase 3: Authentication & Session Management

### 3.1 Authentication Testing
- [ ] **Authentication Bypass**
  - [ ] SQL injection in login forms
  - [ ] NoSQL injection attempts
  - [ ] LDAP injection
  - [ ] Authentication logic flaws
  - [ ] Default credentials testing
  - [ ] Null/empty password attempts

- [ ] **Brute Force Protection**
  - [ ] Account lockout policies
  - [ ] CAPTCHA implementation
  - [ ] Rate limiting effectiveness
  - [ ] IP-based restrictions
  - [ ] Bypass techniques (X-Forwarded-For, etc.)

- [ ] **Password Security**
  - [ ] Password complexity requirements
  - [ ] Password change functionality
  - [ ] Password reset mechanism security
  - [ ] Password storage analysis
  - [ ] Password in URLs or logs

- [ ] **Multi-Factor Authentication**
  - [ ] MFA bypass techniques
  - [ ] Backup code security
  - [ ] SMS-based MFA vulnerabilities
  - [ ] TOTP implementation flaws
  - [ ] MFA recovery process

### 3.2 Session Management
- [ ] **Session Token Security**
  - [ ] Session token randomness
  - [ ] Session token length and entropy
  - [ ] Session token in URLs
  - [ ] HttpOnly and Secure flags
  - [ ] SameSite attribute
  - [ ] Establish how session management is handled (tokens in cookies, tokens in URL)
  - [ ] Check session cookie scope (path and domain)
  - [ ] Check session cookie duration (expires and max-age)

- [ ] **Session Lifecycle**
  - [ ] Session timeout implementation
  - [ ] Session termination on logout
  - [ ] Session termination after maximum lifetime
  - [ ] Session termination after relative timeout
  - [ ] Concurrent session handling
  - [ ] Session fixation vulnerabilities
  - [ ] Session hijacking possibilities
  - [ ] Test if users can have multiple simultaneous sessions
  - [ ] Confirm new session tokens issued on login, role change, and logout
  - [ ] Test for consistent session management across applications with shared session management
  - [ ] Test for session puzzling

- [ ] **Session-Related Attacks**
  - [ ] Test for CSRF and clickjacking
  - [ ] Test for cache management on HTTP (Pragma, Expires, Max-age)
  - [ ] Test for NULL/Invalid Session Cookie handling

### 3.3 OAuth & Third-Party Authentication
- [ ] **OAuth Implementation**
  - [ ] State parameter validation
  - [ ] Redirect URI validation
  - [ ] Access token exposure
  - [ ] Refresh token security
  - [ ] Scope validation

## 🛡️ Phase 4: Authorization & Access Control

### 4.1 Vertical Privilege Escalation
- [ ] **Role-Based Access Control**
  - [ ] Admin functionality exposure
  - [ ] Role manipulation attempts
  - [ ] Function-level access control
  - [ ] API endpoint authorization
  - [ ] Direct object references

### 4.2 Horizontal Privilege Escalation
- [ ] **User Isolation**
  - [ ] IDOR (Insecure Direct Object References)
  - [ ] User data access between accounts
  - [ ] Parameter manipulation
  - [ ] UUID/ID prediction
  - [ ] Path traversal attempts

### 4.3 Access Control Bypass
- [ ] **HTTP Method Tampering**
  - [ ] PUT/DELETE method availability
  - [ ] OPTIONS method information
  - [ ] HEAD method responses
  - [ ] TRACE/TRACK methods

## 💉 Phase 5: Input Validation & Injection Attacks

### 5.1 SQL Injection
- [ ] **Detection Methods**
  - [ ] Error-based SQL injection
  - [ ] Union-based SQL injection
  - [ ] Boolean-based blind SQL injection
  - [ ] Time-based blind SQL injection
  - [ ] Second-order SQL injection

- [ ] **Advanced Techniques**
  - [ ] WAF bypass techniques
  - [ ] Database-specific payloads
  - [ ] NoSQL injection (MongoDB, CouchDB)
  - [ ] ORM injection vulnerabilities
  - [ ] Stored procedure abuse
  - [ ] LDAP injection testing
  - [ ] SQL wildcard DoS testing

### 5.2 Cross-Site Scripting (XSS)
- [ ] **XSS Types**
  - [ ] Reflected XSS
  - [ ] Stored XSS
  - [ ] DOM-based XSS
  - [ ] Blind XSS
  - [ ] Self-XSS with social engineering

- [ ] **XSS Context & Bypass**
  - [ ] HTML context injection
  - [ ] JavaScript context injection
  - [ ] CSS context injection
  - [ ] URL context injection
  - [ ] Filter and WAF bypass

### 5.3 Server-Side Injection
- [ ] **Command Injection**
  - [ ] OS command injection
  - [ ] Blind command injection
  - [ ] Time-based command injection
  - [ ] Command chaining techniques

- [ ] **Server-Side Template Injection (SSTI)**
  - [ ] Template engine detection
  - [ ] Template syntax exploitation
  - [ ] Code execution via templates
  - [ ] Template sandbox escape

- [ ] **XML/XXE Injection**
  - [ ] XML External Entity injection
  - [ ] Blind XXE
  - [ ] XXE via file upload
  - [ ] XXE in SOAP services
  - [ ] XML injection testing

- [ ] **Additional Injection Types**
  - [ ] LDAP injection
  - [ ] XPath injection
  - [ ] XQuery injection
  - [ ] IMAP/SMTP injection
  - [ ] SSI (Server Side Include) injection
  - [ ] Expression Language injection
  - [ ] HTTP parameter pollution
  - [ ] Auto-binding vulnerabilities
  - [ ] Mass Assignment vulnerabilities

### 5.4 File Inclusion & Advanced Attacks
- [ ] **Local File Inclusion (LFI)**
  - [ ] Path traversal attacks
  - [ ] Log poisoning
  - [ ] Session file inclusion
  - [ ] Wrapper-based LFI

- [ ] **Remote File Inclusion (RFI)**
  - [ ] Remote code execution
  - [ ] Data URI inclusion
  - [ ] SMB/UNC path inclusion

- [ ] **Additional Attack Vectors**
  - [ ] HTTP Splitting/Smuggling
  - [ ] HTTP Verb Tampering
  - [ ] Open Redirection
  - [ ] Format String vulnerabilities
  - [ ] Buffer Overflow (Stack, Heap, Integer)
  - [ ] Incubated vulnerabilities
  - [ ] Cross Site Flashing
  - [ ] HTML Injection
  - [ ] Code Injection
  - [ ] Compare client-side and server-side validation rules

## 🌐 Phase 6: Client-Side Security

### 6.1 Cross-Site Request Forgery (CSRF)
- [ ] **CSRF Detection**
  - [ ] Token validation testing
  - [ ] Referer header validation
  - [ ] SameSite cookie testing
  - [ ] State-changing operations

### 6.2 Clickjacking
- [ ] **Frame Busting**
  - [ ] X-Frame-Options bypass
  - [ ] CSP frame-ancestors bypass
  - [ ] UI redressing attacks
  - [ ] Overlay attacks

### 6.3 Content Security Policy (CSP)
- [ ] **CSP Bypass**
  - [ ] Unsafe-inline exploitation
  - [ ] JSONP callback abuse
  - [ ] Base-uri manipulation
  - [ ] Nonce/hash bypass

### 6.4 Cross-Origin Resource Sharing (CORS)
- [ ] **CORS Misconfiguration**
  - [ ] Wildcard origin acceptance
  - [ ] Null origin acceptance
  - [ ] Subdomain trust issues
  - [ ] Credentials exposure

## 📱 Phase 7: Modern Web Application Security

### 7.1 API Security Testing
- [ ] **REST API Testing**
  - [ ] HTTP method manipulation
  - [ ] Parameter pollution
  - [ ] Mass assignment vulnerabilities
  - [ ] API versioning issues
  - [ ] Rate limiting bypass

- [ ] **GraphQL Testing**
  - [ ] Introspection queries
  - [ ] Query depth attacks
  - [ ] Field suggestion attacks
  - [ ] Mutation testing

### 7.2 WebSocket Security
- [ ] **WebSocket Vulnerabilities**
  - [ ] Authentication bypass
  - [ ] Message manipulation
  - [ ] Cross-site WebSocket hijacking
  - [ ] Protocol downgrade attacks

### 7.3 HTML5 Security Features
- [ ] **Web Storage**
  - [ ] LocalStorage security
  - [ ] SessionStorage security
  - [ ] Web SQL injection
  - [ ] IndexedDB security

- [ ] **PostMessage Security**
  - [ ] Origin validation
  - [ ] Message content validation
  - [ ] Postmessage XSS

- [ ] **HTML5 Specific Tests**
  - [ ] Test Web Messaging
  - [ ] Test for Web Storage SQL injection
  - [ ] Check CORS implementation
  - [ ] Check Offline Web Application security

## 🔒 Phase 8: Business Logic & Application-Specific Testing

### 8.1 Business Logic Flaws
- [ ] **Workflow Bypasses**
  - [ ] Multi-step process manipulation
  - [ ] Payment process bypass
  - [ ] Approval workflow bypass
  - [ ] Time-based logic flaws

- [ ] **Race Conditions**
  - [ ] Concurrent request handling
  - [ ] TOCTOU vulnerabilities
  - [ ] Payment race conditions
  - [ ] Coupon/discount abuse

### 8.2 Application-Specific Logic
- [ ] **E-commerce Testing**
  - [ ] Price manipulation
  - [ ] Coupon stacking
  - [ ] Inventory manipulation
  - [ ] Payment bypass

- [ ] **Social Features**
  - [ ] Privacy control bypass
  - [ ] Friend/follower manipulation
  - [ ] Content manipulation
  - [ ] Notification abuse

- [ ] **Enhanced Business Logic Testing**
  - [ ] Test for feature misuse
  - [ ] Test for lack of non-repudiation
  - [ ] Test for trust relationships
  - [ ] Test for integrity of data
  - [ ] Test segregation of duties

## 🔐 Phase 9: Cryptography & Data Protection

### 9.1 Encryption Implementation
- [ ] **Weak Cryptography**
  - [ ] Weak encryption algorithms
  - [ ] Hardcoded encryption keys
  - [ ] Poor key management
  - [ ] Predictable random values
  - [ ] Check if data which should be encrypted is not
  - [ ] Check for wrong algorithms usage depending on context
  - [ ] Check for weak algorithms usage
  - [ ] Check for proper use of salting
  - [ ] Check for randomness functions

### 9.2 Data Exposure
- [ ] **Sensitive Data Exposure**
  - [ ] PII in URLs/logs
  - [ ] Credit card data exposure
  - [ ] Password in plaintext
  - [ ] API keys exposure

## 📤 Phase 10: File Upload & Processing

### 10.1 File Upload Security
- [ ] **Upload Restrictions**
  - [ ] File type validation bypass
  - [ ] File size limit bypass
  - [ ] Filename manipulation
  - [ ] Content-type spoofing
  - [ ] Test that acceptable file types are whitelisted
  - [ ] Test that file size limits, upload frequency and total file counts are defined and enforced
  - [ ] Test that file contents match the defined file type
  - [ ] Test that unsafe filenames are sanitised

- [ ] **Malicious File Upload**
  - [ ] Web shell upload
  - [ ] Executable file upload
  - [ ] Archive bomb attacks
  - [ ] Image-based attacks

- [ ] **File Upload Security Controls**
  - [ ] Test that all file uploads have Anti-Virus scanning in place
  - [ ] Test that uploaded files are not directly accessible within the web root
  - [ ] Test that uploaded files are not served on the same hostname/port
  - [ ] Test that files and media are integrated with authentication and authorization schemas

### 10.2 File Processing
- [ ] **Document Processing**
  - [ ] XXE in document parsers
  - [ ] Macro-enabled documents
  - [ ] PDF-based attacks
  - [ ] Image processing vulnerabilities

## 💳 Phase 10.5: Payment & Card Processing Security

### 10.5.1 Card Payment Testing
- [ ] **Payment Security Assessment**
  - [ ] Test for known vulnerabilities and configuration issues on Web Server and Web Application
  - [ ] Test for default or guessable passwords
  - [ ] Test for non-production data in live environment, and vice-versa
  - [ ] Test for Injection vulnerabilities in payment processing
  - [ ] Test for Buffer Overflows in payment components
  - [ ] Test for Insecure Cryptographic Storage of payment data
  - [ ] Test for Insufficient Transport Layer Protection for payment data
  - [ ] Test for Improper Error Handling in payment flows
  - [ ] Test for all vulnerabilities with a CVSS v2 score > 4.0
  - [ ] Test for Authentication and Authorization issues in payment processes
  - [ ] Test for CSRF in payment operations

## 🚫 Phase 11: Denial of Service Testing

### 11.1 Application-Level DoS
- [ ] **Resource Exhaustion**
  - [ ] Algorithmic complexity attacks
  - [ ] Memory exhaustion
  - [ ] Database connection exhaustion
  - [ ] CPU intensive operations

### 11.2 Specific DoS Vectors
- [ ] **Input-Based DoS**
  - [ ] Regular expression DoS (ReDoS)
  - [ ] XML bomb attacks
  - [ ] Billion laughs attack
  - [ ] Zip bomb uploads

- [ ] **Enhanced DoS Testing**
  - [ ] Test for anti-automation bypasses
  - [ ] Test for account lockout mechanisms
  - [ ] Test for HTTP protocol DoS
  - [ ] Test for SQL wildcard DoS

## 🔍 Phase 12: Advanced Attack Techniques

### 12.1 Deserialization Attacks
- [ ] **Serialization Vulnerabilities**
  - [ ] Java deserialization
  - [ ] Python pickle exploitation
  - [ ] .NET deserialization
  - [ ] PHP object injection

### 12.2 Server-Side Request Forgery (SSRF)
- [ ] **SSRF Detection**
  - [ ] Internal network access
  - [ ] Cloud metadata access
  - [ ] Port scanning via SSRF
  - [ ] Protocol smuggling

### 12.3 HTTP Request Smuggling
- [ ] **Smuggling Techniques**
  - [ ] CL.TE vulnerabilities
  - [ ] TE.CL vulnerabilities
  - [ ] TE.TE vulnerabilities
  - [ ] HTTP/2 downgrade attacks

## 📝 Phase 13: Documentation & Reporting

### 13.1 Evidence Collection
- [ ] **Proof of Concept**
  - [ ] Screenshot documentation
  - [ ] Request/response captures
  - [ ] Video demonstrations
  - [ ] Step-by-step reproduction

### 13.2 Impact Assessment
- [ ] **Risk Evaluation**
  - [ ] Confidentiality impact
  - [ ] Integrity impact
  - [ ] Availability impact
  - [ ] Business impact assessment

### 13.3 Report Writing
- [ ] **Professional Reporting**
  - [ ] Clear vulnerability description
  - [ ] Detailed reproduction steps
  - [ ] Risk assessment
  - [ ] Remediation recommendations
  - [ ] Professional presentation

## 🛠️ Tools & Resources

### Essential Tools
- **Reconnaissance**: Amass, Subfinder, Assetfinder, DNSGen, MassDNS, HTTProbe, Aquatone, Nuclei
- **Web Proxies**: Burp Suite, OWASP ZAP, Caido
- **Scanners**: Nmap, Masscan, Nikto, Dirb/Gobuster, FFUF
- **URL Discovery**: Hakrawler, GAU, ParamSpider, LinkFinder
- **Exploitation**: SQLMap, XSStrike, Commix, wfuzz
- **Mobile**: MobSF, Frida, objection, APKTool
- **Custom**: Custom Python/Bash scripts, API testing tools

### Learning Resources
- **Documentation**: OWASP Testing Guide, Web Security Academy
- **Practice**: DVWA, WebGoat, HackTheBox, TryHackMe
- **Communities**: Bug bounty forums, Discord/Slack channels
- **Blogs**: Security researcher blogs, writeups, methodologies

## ⚠️ Important Notes

1. **Always follow program rules and scope**
2. **Avoid testing on production systems unnecessarily**
3. **Respect rate limits and don't cause service disruption**
4. **Document everything for proper reporting**
5. **Stay updated with latest vulnerabilities and techniques**
6. **Practice responsible disclosure**
7. **Continuous learning is key to success**

---
*This checklist is compiled from 5+ comprehensive sources including OWASP guidelines, expert methodologies, community repositories (sehno, 0xRadi, shubhamrooter, alihussainzada), and bug bounty best practices. Regular updates recommended as new attack vectors emerge.*
