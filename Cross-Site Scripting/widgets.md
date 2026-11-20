## Title
Reflected XSS - Reddit

## Description
**Affected URL:** https://widgets.pwnedbox.site/

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the application's URL path, where user-controlled input is reflected into the HTTP response without proper output encoding. An attacker can craft a malicious URL to execute arbitrary JavaScript in a victim's browser when visited.

## Steps to Reproduce
1. Open the following URL in a browser: `https://widgets.pwnedbox.site/index.php/svc/shreddit/api/comments/askreddit/t3_u9po1lrix4uni'"<><img src=x onerror=alert(1)>/t1_i5sxroa`
2. Observe that the JavaScript payload executes and triggers an alert box (`1`), confirming reflected XSS execution

## POC (Proof of Concept)
<img width="1291" height="903" alt="image" src="https://github.com/user-attachments/assets/c626b7fa-7671-4d3e-b1c6-eb912b2ffd6a" />
<img width="1775" height="1020" alt="image" src="https://github.com/user-attachments/assets/37287640-9ca4-41b0-bc63-600e48da9e9b" />

## Impact
- It allows attackers to hijack user session
- It potentially leads to full account takeover
- It allows to perform  unauthorized actions within the vulnerable application

## Remediation
- Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
- Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
- If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
- Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server
