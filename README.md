# 🐛 Comprehensive Bug Hunting Checklist v2.0

[![Version](https://img.shields.io/badge/version-2.0-blue.svg)](https://github.com/yourusername/bug-hunting-checklist)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![OWASP](https://img.shields.io/badge/OWASP-compliant-red.svg)](https://owasp.org/www-project-web-security-testing-guide/)

> A comprehensive, methodical approach to bug hunting and penetration testing compiled from OWASP guidelines, expert methodologies, and community best practices.

## ⚡ Quick Info

**⏱️ Creation Time:** ~17 minute ( Ik , it's quite long )
**🤖 Generated with:** Claude 4 (Sonnet)  
**📚 Sources:** Multiple web searches, Medium articles, security blogs, and community resources  
**👥 Credits:** All credits to original authors - see [Credits](https://github.com/gigachad80/Checklist/blob/main/README.md#-credits-) section

---

When you have completed an action, don't forget to check it off! ✅  
Happy hunting! 🎯🎯

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

---

## 🔍 Phase 1: Reconnaissance & Information Gathering

<details>
<summary><strong>1.1 Passive Reconnaissance</strong></summary>

### Wildcard Domain Reconnaissance
- [ ] Run [Amass](https://github.com/OWASP/Amass) for comprehensive subdomain enumeration
  ```bash
  amass enum -d target.com -o amass_output.txt
  ```
- [ ] Use [Subfinder](https://github.com/projectdiscovery/subfinder) for fast subdomain discovery
  ```bash
  subfinder -d target.com -o subfinder_output.txt
  ```
- [ ] Execute [Assetfinder](https://github.com/tomnomnom/assetfinder) for additional subdomain sources
  ```bash
  assetfinder target.com > assetfinder_output.txt
  ```
- [ ] Run [DNSGen](https://github.com/ProjectAnte/dnsgen) for subdomain permutation generation
  ```bash
  dnsgen wordlist.txt > dnsgen_output.txt
  ```
- [ ] Use [MassDNS](https://github.com/blechschmidt/massdns) for bulk DNS resolution
  ```bash
  massdns -r resolvers.txt -t A -o S subdomains.txt
  ```
- [ ] Apply [HTTProbe](https://github.com/tomnomnom/httprobe) to check for live hosts
  ```bash
  cat subdomains.txt | httprobe > live_hosts.txt
  ```
- [ ] Run [Aquatone](https://github.com/michenriksen/aquatone) for visual screenshots of alive hosts
  ```bash
  cat live_hosts.txt | aquatone
  ```

### Single Domain Scanning
- [ ] Comprehensive [Nmap](https://nmap.org/) scan with service detection
  ```bash
  nmap -sS -sV -sC -A -oA nmap_scan target.com
  ```
- [ ] [Burp Suite](https://portswigger.net/burp) crawler for comprehensive mapping
- [ ] [FFUF](https://github.com/ffuf/ffuf) for directory and file fuzzing
  ```bash
  ffuf -w wordlist.txt -u https://target.com/FUZZ
  ```
- [ ] [Hakrawler](https://github.com/hakluke/hakrawler)/[GAU](https://github.com/lc/gau)/[ParamSpider](https://github.com/devanshbatham/ParamSpider) for URL discovery
- [ ] [LinkFinder](https://github.com/GerbenJavado/LinkFinder) for endpoint discovery in JavaScript
- [ ] Extract URLs from Android applications (if applicable)

### Manual Intelligence Gathering
- [ ] [Shodan](https://shodan.io/) reconnaissance for exposed services
- [ ] [Censys](https://censys.io/) search for certificates and services
- [ ] Google dorking for exposed files/directories
- [ ] [Pastebin](https://pastebin.com/) searches for leaked credentials
- [ ] [GitHub](https://github.com/)/[GitLab](https://gitlab.com/) code search for secrets and endpoints
- [ ] OSINT gathering from multiple sources

### Domain Enumeration
- [ ] Subdomain discovery using multiple sources ([crt.sh](https://crt.sh/), [Subfinder](https://github.com/projectdiscovery/subfinder), [Amass](https://github.com/OWASP/Amass))
- [ ] Check DNS records (A, AAAA, CNAME, MX, TXT, NS)
- [ ] Reverse DNS lookups
- [ ] ASN enumeration for related IP ranges
- [ ] Check for wildcard subdomains

### Search Engine Intelligence
- [ ] Google dorking for exposed files/directories
- [ ] Bing, DuckDuckGo, Yandex searches
- [ ] Check [archive.org](https://archive.org/) for historical data
- [ ] [GitHub](https://github.com/)/[GitLab](https://gitlab.com/) code search for secrets
- [ ] [Shodan](https://shodan.io/)/[Censys](https://censys.io/) for exposed services

### Social Media & Public Information
- [ ] LinkedIn employee enumeration
- [ ] Twitter/social media mentions
- [ ] Job postings for technology stack info
- [ ] Company blog posts and documentation
- [ ] Public presentations and conferences

</details>

<details>
<summary><strong>1.2 Active Reconnaissance</strong></summary>

### Port Scanning & Service Detection
- [ ] [Nmap](https://nmap.org/) comprehensive scan (-sS, -sV, -sC, -A)
- [ ] UDP port scanning for common services
- [ ] Service version identification
- [ ] Default credential testing

### Web Application Discovery
- [ ] Directory/file brute forcing ([Gobuster](https://github.com/OJ/gobuster), [Dirb](https://github.com/v0re/dirb), [Dirsearch](https://github.com/maurosoria/dirsearch))
- [ ] Technology stack identification ([Wappalyzer](https://www.wappalyzer.com/), [BuiltWith](https://builtwith.com/))
- [ ] CMS detection and version identification
- [ ] Check for common files (robots.txt, sitemap.xml, .well-known/)
- [ ] Backup file discovery (.bak, .old, .tmp, ~)

</details>

<details>
<summary><strong>1.3 Application Mapping</strong></summary>

### Manual Exploration
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

### Automated Spidering
- [ ] [Burp Suite](https://portswigger.net/burp) spider/crawler
- [ ] [OWASP ZAP](https://owasp.org/www-project-zap/) automated scan
- [ ] Custom crawler scripts
- [ ] JavaScript analysis for hidden endpoints

### Content Discovery
- [ ] Check for files that expose content (robots.txt, sitemap.xml, .DS_Store)
- [ ] Check caches of major search engines for publicly accessible sites
- [ ] Test for differences in content based on User Agent (Mobile sites, search engine crawler access)
- [ ] Perform comprehensive web application fingerprinting

</details>

---

## 🔧 Phase 2: Configuration & Infrastructure Testing

<details>
<summary><strong>2.1 Server Configuration</strong></summary>

### HTTP Security Headers
- [ ] X-Frame-Options (Clickjacking protection)
- [ ] X-XSS-Protection
- [ ] X-Content-Type-Options
- [ ] Content-Security-Policy (CSP)
- [ ] Strict-Transport-Security (HSTS)
- [ ] Referrer-Policy
- [ ] Permissions-Policy/Feature-Policy

### SSL/TLS Configuration
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

### Server Information Disclosure
- [ ] Server version in headers
- [ ] Technology stack fingerprinting
- [ ] Error message information disclosure
- [ ] Debug information exposure
- [ ] Source code comments
- [ ] Check for sensitive data in client-side code (API keys, credentials)

### HTTP Methods & Configuration
- [ ] Check HTTP methods supported and Cross Site Tracing (XST)
- [ ] Test file extensions handling
- [ ] Test for policies (Flash, Silverlight, robots)
- [ ] Test for non-production data in live environment

</details>

<details>
<summary><strong>2.2 Access Controls & Permissions</strong></summary>

### File & Directory Permissions
- [ ] Sensitive file exposure
- [ ] Directory listing enabled
- [ ] Backup file accessibility
- [ ] Configuration file exposure
- [ ] Log file accessibility
- [ ] Check for commonly used application and administrative URLs
- [ ] Check for old, backup and unreferenced files

</details>

---

## 🔐 Phase 3: Authentication & Session Management

<details>
<summary><strong>3.1 Authentication Testing</strong></summary>

### Authentication Bypass
- [ ] SQL injection in login forms
- [ ] NoSQL injection attempts
- [ ] LDAP injection
- [ ] Authentication logic flaws
- [ ] Default credentials testing
- [ ] Null/empty password attempts

### Brute Force Protection
- [ ] Account lockout policies
- [ ] CAPTCHA implementation
- [ ] Rate limiting effectiveness
- [ ] IP-based restrictions
- [ ] Bypass techniques (X-Forwarded-For, etc.)

### Password Security
- [ ] Password complexity requirements
- [ ] Password change functionality
- [ ] Password reset mechanism security
- [ ] Password storage analysis
- [ ] Password in URLs or logs

### Multi-Factor Authentication
- [ ] MFA bypass techniques
- [ ] Backup code security
- [ ] SMS-based MFA vulnerabilities
- [ ] TOTP implementation flaws
- [ ] MFA recovery process

</details>

<details>
<summary><strong>3.2 Session Management</strong></summary>

### Session Token Security
- [ ] Session token randomness
- [ ] Session token length and entropy
- [ ] Session token in URLs
- [ ] HttpOnly and Secure flags
- [ ] SameSite attribute
- [ ] Establish how session management is handled (tokens in cookies, tokens in URL)
- [ ] Check session cookie scope (path and domain)
- [ ] Check session cookie duration (expires and max-age)

### Session Lifecycle
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

### Session-Related Attacks
- [ ] Test for CSRF and clickjacking
- [ ] Test for cache management on HTTP (Pragma, Expires, Max-age)
- [ ] Test for NULL/Invalid Session Cookie handling

</details>

<details>
<summary><strong>3.3 OAuth & Third-Party Authentication</strong></summary>

### OAuth Implementation
- [ ] State parameter validation
- [ ] Redirect URI validation
- [ ] Access token exposure
- [ ] Refresh token security
- [ ] Scope validation

</details>

---

## 🛡️ Phase 4: Authorization & Access Control

<details>
<summary><strong>4.1 Vertical Privilege Escalation</strong></summary>

### Role-Based Access Control
- [ ] Admin functionality exposure
- [ ] Role manipulation attempts
- [ ] Function-level access control
- [ ] API endpoint authorization
- [ ] Direct object references

</details>

<details>
<summary><strong>4.2 Horizontal Privilege Escalation</strong></summary>

### User Isolation
- [ ] IDOR (Insecure Direct Object References)
- [ ] User data access between accounts
- [ ] Parameter manipulation
- [ ] UUID/ID prediction
- [ ] Path traversal attempts

</details>

<details>
<summary><strong>4.3 Access Control Bypass</strong></summary>

### HTTP Method Tampering
- [ ] PUT/DELETE method availability
- [ ] OPTIONS method information
- [ ] HEAD method responses
- [ ] TRACE/TRACK methods

</details>

---

## 💉 Phase 5: Input Validation & Injection Attacks

<details>
<summary><strong>5.1 SQL Injection</strong></summary>

### Detection Methods
- [ ] Error-based SQL injection
- [ ] Union-based SQL injection
- [ ] Boolean-based blind SQL injection
- [ ] Time-based blind SQL injection
- [ ] Second-order SQL injection

### Advanced Techniques
- [ ] WAF bypass techniques
- [ ] Database-specific payloads
- [ ] NoSQL injection (MongoDB, CouchDB)
- [ ] ORM injection vulnerabilities
- [ ] Stored procedure abuse
- [ ] LDAP injection testing
- [ ] SQL wildcard DoS testing

</details>

<details>
<summary><strong>5.2 Cross-Site Scripting (XSS)</strong></summary>

### XSS Types
- [ ] Reflected XSS
- [ ] Stored XSS
- [ ] DOM-based XSS
- [ ] Blind XSS
- [ ] Self-XSS with social engineering

### XSS Context & Bypass
- [ ] HTML context injection
- [ ] JavaScript context injection
- [ ] CSS context injection
- [ ] URL context injection
- [ ] Filter and WAF bypass

</details>

<details>
<summary><strong>5.3 Server-Side Injection</strong></summary>

### Command Injection
- [ ] OS command injection
- [ ] Blind command injection
- [ ] Time-based command injection
- [ ] Command chaining techniques

### Server-Side Template Injection (SSTI)
- [ ] Template engine detection
- [ ] Template syntax exploitation
- [ ] Code execution via templates
- [ ] Template sandbox escape

### XML/XXE Injection
- [ ] XML External Entity injection
- [ ] Blind XXE
- [ ] XXE via file upload
- [ ] XXE in SOAP services
- [ ] XML injection testing

### Additional Injection Types
- [ ] LDAP injection
- [ ] XPath injection
- [ ] XQuery injection
- [ ] IMAP/SMTP injection
- [ ] SSI (Server Side Include) injection
- [ ] Expression Language injection
- [ ] HTTP parameter pollution
- [ ] Auto-binding vulnerabilities
- [ ] Mass Assignment vulnerabilities

</details>

<details>
<summary><strong>5.4 File Inclusion & Advanced Attacks</strong></summary>

### Local File Inclusion (LFI)
- [ ] Path traversal attacks
- [ ] Log poisoning
- [ ] Session file inclusion
- [ ] Wrapper-based LFI

### Remote File Inclusion (RFI)
- [ ] Remote code execution
- [ ] Data URI inclusion
- [ ] SMB/UNC path inclusion

### Additional Attack Vectors
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

</details>

---

## 🌐 Phase 6: Client-Side Security

<details>
<summary><strong>6.1 Cross-Site Request Forgery (CSRF)</strong></summary>

### CSRF Detection
- [ ] Token validation testing
- [ ] Referer header validation
- [ ] SameSite cookie testing
- [ ] State-changing operations

</details>

<details>
<summary><strong>6.2 Clickjacking</strong></summary>

### Frame Busting
- [ ] X-Frame-Options bypass
- [ ] CSP frame-ancestors bypass
- [ ] UI redressing attacks
- [ ] Overlay attacks

</details>

<details>
<summary><strong>6.3 Content Security Policy (CSP)</strong></summary>

### CSP Bypass
- [ ] Unsafe-inline exploitation
- [ ] JSONP callback abuse
- [ ] Base-uri manipulation
- [ ] Nonce/hash bypass

</details>

<details>
<summary><strong>6.4 Cross-Origin Resource Sharing (CORS)</strong></summary>

### CORS Misconfiguration
- [ ] Wildcard origin acceptance
- [ ] Null origin acceptance
- [ ] Subdomain trust issues
- [ ] Credentials exposure

</details>

---

## 📱 Phase 7: Modern Web Application Security

<details>
<summary><strong>7.1 API Security Testing</strong></summary>

### REST API Testing
- [ ] HTTP method manipulation
- [ ] Parameter pollution
- [ ] Mass assignment vulnerabilities
- [ ] API versioning issues
- [ ] Rate limiting bypass

### GraphQL Testing
- [ ] Introspection queries
- [ ] Query depth attacks
- [ ] Field suggestion attacks
- [ ] Mutation testing

</details>

<details>
<summary><strong>7.2 WebSocket Security</strong></summary>

### WebSocket Vulnerabilities
- [ ] Authentication bypass
- [ ] Message manipulation
- [ ] Cross-site WebSocket hijacking
- [ ] Protocol downgrade attacks

</details>

<details>
<summary><strong>7.3 HTML5 Security Features</strong></summary>

### Web Storage
- [ ] LocalStorage security
- [ ] SessionStorage security
- [ ] Web SQL injection
- [ ] IndexedDB security

### PostMessage Security
- [ ] Origin validation
- [ ] Message content validation
- [ ] Postmessage XSS

### HTML5 Specific Tests
- [ ] Test Web Messaging
- [ ] Test for Web Storage SQL injection
- [ ] Check CORS implementation
- [ ] Check Offline Web Application security

</details>

---

## 🔒 Phase 8: Business Logic & Application-Specific Testing

<details>
<summary><strong>8.1 Business Logic Flaws</strong></summary>

### Workflow Bypasses
- [ ] Multi-step process manipulation
- [ ] Payment process bypass
- [ ] Approval workflow bypass
- [ ] Time-based logic flaws

### Race Conditions
- [ ] Concurrent request handling
- [ ] TOCTOU vulnerabilities
- [ ] Payment race conditions
- [ ] Coupon/discount abuse

</details>

<details>
<summary><strong>8.2 Application-Specific Logic</strong></summary>

### E-commerce Testing
- [ ] Price manipulation
- [ ] Coupon stacking
- [ ] Inventory manipulation
- [ ] Payment bypass

### Social Features
- [ ] Privacy control bypass
- [ ] Friend/follower manipulation
- [ ] Content manipulation
- [ ] Notification abuse

### Enhanced Business Logic Testing
- [ ] Test for feature misuse
- [ ] Test for lack of non-repudiation
- [ ] Test for trust relationships
- [ ] Test for integrity of data
- [ ] Test segregation of duties

</details>

---

## 🔐 Phase 9: Cryptography & Data Protection

<details>
<summary><strong>9.1 Encryption Implementation</strong></summary>

### Weak Cryptography
- [ ] Weak encryption algorithms
- [ ] Hardcoded encryption keys
- [ ] Poor key management
- [ ] Predictable random values
- [ ] Check if data which should be encrypted is not
- [ ] Check for wrong algorithms usage depending on context
- [ ] Check for weak algorithms usage
- [ ] Check for proper use of salting
- [ ] Check for randomness functions

</details>

<details>
<summary><strong>9.2 Data Exposure</strong></summary>

### Sensitive Data Exposure
- [ ] PII in URLs/logs
- [ ] Credit card data exposure
- [ ] Password in plaintext
- [ ] API keys exposure

</details>

---

## 📤 Phase 10: File Upload & Processing

<details>
<summary><strong>10.1 File Upload Security</strong></summary>

### Upload Restrictions
- [ ] File type validation bypass
- [ ] File size limit bypass
- [ ] Filename manipulation
- [ ] Content-type spoofing
- [ ] Test that acceptable file types are whitelisted
- [ ] Test that file size limits, upload frequency and total file counts are defined and enforced
- [ ] Test that file contents match the defined file type
- [ ] Test that unsafe filenames are sanitised

### Malicious File Upload
- [ ] Web shell upload
- [ ] Executable file upload
- [ ] Archive bomb attacks
- [ ] Image-based attacks

### File Upload Security Controls
- [ ] Test that all file uploads have Anti-Virus scanning in place
- [ ] Test that uploaded files are not directly accessible within the web root
- [ ] Test that uploaded files are not served on the same hostname/port
- [ ] Test that files and media are integrated with authentication and authorization schemas

</details>

<details>
<summary><strong>10.2 File Processing</strong></summary>

### Document Processing
- [ ] XXE in document parsers
- [ ] Macro-enabled documents
- [ ] PDF-based attacks
- [ ] Image processing vulnerabilities

</details>

---

## 💳 Phase 10.5: Payment & Card Processing Security

<details>
<summary><strong>10.5.1 Card Payment Testing</strong></summary>

### Payment Security Assessment
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

</details>

---

## 🚫 Phase 11: Denial of Service Testing

<details>
<summary><strong>11.1 Application-Level DoS</strong></summary>

### Resource Exhaustion
- [ ] Algorithmic complexity attacks
- [ ] Memory exhaustion
- [ ] Database connection exhaustion
- [ ] CPU intensive operations

</details>

<details>
<summary><strong>11.2 Specific DoS Vectors</strong></summary>

### Input-Based DoS
- [ ] Regular expression DoS (ReDoS)
- [ ] XML bomb attacks
- [ ] Billion laughs attack
- [ ] Zip bomb uploads

### Enhanced DoS Testing
- [ ] Test for anti-automation bypasses
- [ ] Test for account lockout mechanisms
- [ ] Test for HTTP protocol DoS
- [ ] Test for SQL wildcard DoS

</details>

---

## 🔍 Phase 12: Advanced Attack Techniques

<details>
<summary><strong>12.1 Deserialization Attacks</strong></summary>

### Serialization Vulnerabilities
- [ ] Java deserialization
- [ ] Python pickle exploitation
- [ ] .NET deserialization
- [ ] PHP object injection

</details>

<details>
<summary><strong>12.2 Server-Side Request Forgery (SSRF)</strong></summary>

### SSRF Detection
- [ ] Internal network access
- [ ] Cloud metadata access
- [ ] Port scanning via SSRF
- [ ] Protocol smuggling

</details>

<details>
<summary><strong>12.3 HTTP Request Smuggling</strong></summary>

### Smuggling Techniques
- [ ] CL.TE vulnerabilities
- [ ] TE.CL vulnerabilities
- [ ] TE.TE vulnerabilities
- [ ] HTTP/2 downgrade attacks

</details>

---

## 📝 Phase 13: Documentation & Reporting

<details>
<summary><strong>13.1 Evidence Collection</strong></summary>

### Proof of Concept
- [ ] Screenshot documentation
- [ ] Request/response captures
- [ ] Video demonstrations
- [ ] Step-by-step reproduction

</details>

<details>
<summary><strong>13.2 Impact Assessment</strong></summary>

### Risk Evaluation
- [ ] Confidentiality impact
- [ ] Integrity impact
- [ ] Availability impact
- [ ] Business impact assessment

</details>

<details>
<summary><strong>13.3 Report Writing</strong></summary>

### Professional Reporting
- [ ] Clear vulnerability description
- [ ] Detailed reproduction steps
- [ ] Risk assessment
- [ ] Remediation recommendations
- [ ] Professional presentation

</details>

---

## 🛠️ Tools & Resources

### Essential Tools
- **Reconnaissance**: [Amass](https://github.com/OWASP/Amass), [Subfinder](https://github.com/projectdiscovery/subfinder), [Assetfinder](https://github.com/tomnomnom/assetfinder), [DNSGen](https://github.com/ProjectAnte/dnsgen), [MassDNS](https://github.com/blechschmidt/massdns), [HTTProbe](https://github.com/tomnomnom/httprobe), [Aquatone](https://github.com/michenriksen/aquatone), [Nuclei](https://github.com/projectdiscovery/nuclei)
- **Web Proxies**: [Burp Suite](https://portswigger.net/burp), [OWASP ZAP](https://owasp.org/www-project-zap/), [Caido](https://caido.io/)
- **Scanners**: [Nmap](https://nmap.org/), [Masscan](https://github.com/robertdavidgraham/masscan), [Nikto](https://cirt.net/Nikto2), [Dirb](https://github.com/v0re/dirb)/[Gobuster](https://github.com/OJ/gobuster), [FFUF](https://github.com/ffuf/ffuf)
- **URL Discovery**: [Hakrawler](https://github.com/hakluke/hakrawler), [GAU](https://github.com/lc/gau), [ParamSpider](https://github.com/devanshbatham/ParamSpider), [LinkFinder](https://github.com/GerbenJavado/LinkFinder)
- **Exploitation**: [SQLMap](https://github.com/sqlmapproject/sqlmap), [XSStrike](https://github.com/s0md3v/XSStrike), [Commix](https://github.com/commixproject/commix), [wfuzz](https://github.com/xmendez/wfuzz)
- **Mobile**: [MobSF](https://github.com/MobSF/Mobile-Security-Framework-MobSF), [Frida](https://frida.re/), [objection](https://github.com/sensepost/objection), [APKTool](https://ibotpeaches.github.io/Apktool/)
- **Custom**: Custom Python/Bash scripts, API testing tools

### Learning Resources
- **Documentation**: [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/), [Web Security Academy](https://portswigger.net/web-security)
- **Practice**: [DVWA](https://github.com/digininja/DVWA), [WebGoat](https://github.com/WebGoat/WebGoat), [HackTheBox](https://www.hackthebox.com/), [TryHackMe](https://tryhackme.com/)
- **Communities**: Bug bounty forums, Discord/Slack channels
- **Blogs**: Security researcher blogs, writeups, methodologies

---

## ⚠️ Important Notes

1. **Always follow program rules and scope**
2. **Avoid testing on production systems unnecessarily**
3. **Respect rate limits and don't cause service disruption**
4. **Document everything for proper reporting**
5. **Stay updated with latest vulnerabilities and techniques**
6. **Practice responsible disclosure**
7. **Continuous learning is key to success**

---

## 🤝 Contributing

We welcome contributions from the security community! Please read our [Contributing Guidelines](CONTRIBUTING.md) before submitting.

### How to Contribute
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

### 💗 Credits : 
- [sehno](https://github.com/sehno) - Original methodology contributor
- [0xRadi](https://github.com/0xRadi) - Bug hunting techniques
- [shubhamrooter](https://github.com/shubhamrooter) - Testing methodologies
- [alihussainzada](https://github.com/alihussainzada) - Community contributions

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏  Acknowledgements :

*This checklist is compiled from multiple comprehensive sources including OWASP guidelines, expert methodologies, community repositories, and bug bounty best practices. Regular updates recommended as new attack vectors emerge.*

**Version 2.0 Updates:**
- Enhanced reconnaissance methodology with specific tools
- Added comprehensive single domain scanning approach
- Integrated manual intelligence gathering techniques
- Enhanced session management testing
- Expanded injection testing coverage
- Added specific payment security testing section
- Improved file upload security testing
- Enhanced HTML5 security testing
- Updated toolset recommendations

---

**⭐ Star this repository if you find it helpful!**

**🔄 Keep this checklist updated by watching for new releases**
