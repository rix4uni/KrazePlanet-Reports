## Title
Reflected XSS - TutorialRepublic: Web Development Reference Search

## Description
**Affected URL:** https://tutorialrepublic.pwnedbox.site/

A Reflected Cross-Site Scripting (XSS) vulnerability exists in the `q` parameter of the application. User-controlled input is reflected into the response without proper sanitization, allowing arbitrary JavaScript execution in the victim’s browser.

## Steps to Reproduce
1. Open the following URL in a browser: `https://tutorialrepublic.pwnedbox.site/?q=rix4uni1'"<><script>confirm(1)</script>`
2. Observe that the JavaScript payload executes and triggers an alert box (`1`), confirming reflected XSS execution

## POC (Proof of Concept)
<img width="1468" height="851" alt="image" src="https://github.com/user-attachments/assets/ba2fda19-db3e-4050-99ff-cde1017a0bea" />
<img width="1474" height="506" alt="image" src="https://github.com/user-attachments/assets/437eb644-e2fd-464f-aa6c-35864007dc4a" />


## Impact
- It allows attackers to hijack user session
- It potentially leads to full account takeover
- It allows to perform  unauthorized actions within the vulnerable application

## Remediation
- Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
- Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
- If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
- Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server
