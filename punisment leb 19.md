## Title

 Reflected Cross-Site Scripting (XSS) via search Parameter on Help Center Page

## Vulnerability Type

Reflected XSS

## Summary : 
http://kzlabs.com/punishment/19.php categoryid parameter is vulnerable to reflected XSS . website reflects the User input from search paramter . which leads attacker to add malecious javascript code within victims browser when user visit malecious url . 

## Vulnerable Endpoint
http://kzlabs.com/punishment/19.php?categoryid=

## Steps to Reproduce : 

1. Navigate to the following URL : ```http://kzlabs.com/punishment/19.php?categoryid=<img src=x onerror="aalertlert(1)">```
2. Observe that a JavaScript alert box pops up displaying `1` — confirming that the script executed.
   


## Payload Used

```<img src=x onerror="aalertlert(1)">```

## Proof of Concept Request
  ```Screemshot 1 : ``` TThe Report Shows Payload add in search bar . Location where payload should be insert. 
<img width="1920" height="1080" alt="Screenshot From 2026-05-25 21-49-01" src="https://github.com/user-attachments/assets/3ba680c0-8adf-4e9c-abc8-ac403808ab09" />


 ```Screenshot 2 : ``` The Report Shows Successfully the Payload has worked and Pop up Box get Fired.
 
 
<img width="1920" height="1080" alt="Screenshot From 2026-05-25 21-48-46" src="https://github.com/user-attachments/assets/28687a30-7ce3-429f-a331-058ccbb952d0" />



## Impact
 
 An attacker can perform the following actions using this vulnerability:
  - It allows attackers to hijack user session
  - It potentially leads to full account takeover
  - It allows to perform  unauthorized actions within the vulnerable application
  - It allows attacker to exfiltrate sensitive data
  
## Recommendations for fix:

 Validate and sanitize the redirectUrl parameter to ensure that it does not contain any malicious content. This can be done by:

1. Filter out HTML tags like: `<script>`, `<img>`, `<svg>` from the Report Name field before saving anything to the database
2. Filter out JavaScript methods like: `alert()`, `confirm()`, `prompt()` so even if a tag slips through the method won't execute
4. If you're using PHP then use `htmlspecialchars()` function before rendering any user input back to the page
5. Use Cloudflare as they have so many WAF rules that almost all XSS payloads will be blocked automatically before even reaching the server


