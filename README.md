# Project 8 - Pen Testing Live Targets

Time spent: **6** hours spent in total

<h2>**Homework Instructions**:</h2> 
For this week's assignment, discover and demonstrate similar proofs-of-concept for at least an additional three and (up to five) exploits affecting an older version of WP.

Challenge Goals:

Out of the following goals you must complete any 3 challenges:

1. Username Enumeration: A careless developer mistake has created a username enumeration vulnerability. Determine which color has the vulnerability. You can use the existing username "jmonroe99" as a test. Next, figure out what mistake the developer made.

2. Insecure Direct Object Reference: One of the three sites is missing code which would prevent some sensitive information from being made public. Determine which color has the vulnerability. Then, figure out what the other two sites did correctly to prevent the information leak.

3. SQL Injection: Most of the data input received by these websites is being sanitized properly. However, one of the three sites has one place where the input is not being sanitized before being used in an SQL query. Determine which color has the vulnerability.

4. Cross-Site Scripting: All three sites do a good job of protecting against a reflected XSS attack. However, one of the sites has a mistake which leaves the site vulnerable to a stored XSS attack. A reflected XSS attack would be easy to reveal, while a stored XSS does not provide instant feedback. You will need to log into the admin area and look through the CMS in order to "spring the trap" and find out if your attack succeeded. Determine which color has the vulnerability. Remember, others will be attacking these sites alongside you. Use your name in the XSS so that your results won't be confused with anyone else's (example: <script>alert('Mallory found the XSS!');</script>).

5. Cross-Site Request Forgery: One of the three sites does not have CSRF protections on the admin area. A clever attacker could design a form which would automatically submit form data to the staff area and take advantage of a logged in user's access permissions. Be the attacker and design a form which will make a change to the spelling of some database content. (For example, change the first user from "James" to "Jim", or change "Alabama" to "Alabamaaaa"). Then point the form action at each of the three sites to find out which color has the vulnerability. Do not neglect to be stealthy with your form—your unsuspecting, logged-in admin should neither see the form nor the results of the form submission.

6. Session Hijacking/Fixation: Two of the three websites expire their active sessions and require users to re-login every 30 minutes. That is probably too aggressive for the real world, but it is better than the third site which allows sessions to be a year old, and never regenerates the session ID, even when the user agent string changes. This makes it vulnerable to both session hijacking and session fixation attacks.

There are many ways an attacker could get or set the session ID in the real world (XSS, sniffing WiFi packets, etc.). For this exercise, a PHP script has been provided to help you, "public/hacktools/change_session_id.php". You can load this script to find out the current session ID or to set it to a new one.

Use two different web browsers (e.g., Firefox and Chrome). Let one browser be the attacker and the other the target. Choose if you want to attempt a session hijacking or session fixation. For hijacking, log the target in first, then give the logged-in session ID to the attacker. For fixation, get a session ID for the attacker, give it to the target, then the target will log in. In both cases, the attacker should now have access to the staff area.

Determine which color has the vulnerability.





<h2>Green Exploits</h2>
<h3>User Enumeration</h3>
<img src="Week 8 Green Enum.gif" alt="Enum">
<h3>Cross Site Scripting</h3>
<img src="Week 8 Green XSS.gif" alt="XSS">

<h2>Blue Exploits</h2>
<h3>Session Hijacking</h3>
<img src="Week 8 Blue Hijack.gif" alt="Hijack">
<h3>SQL Injection</h3>
<img src="Week 8 Blue SQLi.gif" alt="SQLi">

<h2>Red Exploits</h2>
<h3>Indirect Object Reference</h3>
<img src="Week 8 Red IDOR.gif" alt="IDOR">
<h3>Cross Site Request Forgery</h3>
<img src="Week 8 Red CSRF.gif" alt="CSRF">
