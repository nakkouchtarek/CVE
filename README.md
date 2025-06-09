### Summary
A stored Cross-Site Scripting (XSS) vulnerability in the tags meta configuration robots field allows users with permissions ( administrators mainly ) to inject malicious JavaScript that persists across all pages where the meta robots tag is rendered, compromising other administrator sessions or other users that visit the wiki on the spot.

### Details
The tags meta configuration panel contains an input field for setting meta robots tag that does not properly sanitze user input. When an administrator enters Javascript code in there, it will get loaded in the meta field directly for any other session and thus impact any other user. 

### PoC

* Login as your admin account or a user that has read/write to meta tags
* Go to Gestion de site -> Fichier de conf -> Tags meta for web indexing
* In the meta[robots] field input the following payload: `"><script>alert(1)</script>`

![image](https://github.com/user-attachments/assets/32bedee7-e783-488b-a8fa-58f11addb358)

* Submit and now when you visit any other page you'll get an alert

![image](https://github.com/user-attachments/assets/338d9854-8469-4043-9eb6-f2ed10548507)

### Impact

This stored XSS vulnerability affects all users since it executes on every page a user visits through the meta tag. An attacker through it can hijack user sessions, perform unauthorized actions through malicious scripts, steal credentials, and compromise other administrator / user accounts to gain persistent access.
