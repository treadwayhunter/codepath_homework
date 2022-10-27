See branches for assignments.

# Project 7 - WordPress vs Kali

Time spent: **11** hours spent in total

<h2>**Homework Instructions**:</h2> 
For this week's assignment, discover and demonstrate similar proofs-of-concept for at least an additional three and (up to five) exploits affecting an older version of WP.

You can use any version of WP you like, though keep in mind that the WPDistillery setup will be less reliable for very old versions, and you may have to dive into the WP setup for versions much older than 4.x
Bonus points for Core WP exploits, but if you're having trouble identifying enough of them, you can try installing some plugins / themes to open up the attack surface -- just be sure to note this in your writeup
Try to find exploits that cover some of the different techniques we've worked with so far:
- XSS
- SQLI
- CSRF
- User Enumeration
- Privilege Escalation

You should be able to recreate most exploits via the browser running on your local machine. You can use Kali to run wpscan (or other auditing tools you can find) to do recon, but most exploits should be demonstrable via the browser
For each exploit, provide the following information in the README.md:
- A small writeup indicating the steps you used to recreate
- The types / classes of vulnerabilities involved and any related CVE identifiers
- Identify affected versions and patches
- Links to the source code, where possible
- A screen cap


<h2>**User Enumeration**</h2>
After doing some research, it turns out that every version of WordPress by default is susceptible to user enumeration. This can be fixed, but requires manually changing some of the source code. The wpscan tool on Kali has a built in feature specifically for user enumeration and can be used to determine if a particular WordPress setup is susceptible or not.

1)	Open Kali Linux Terminal
2)	Run the command 
•	wpscan –url <URL or IP address of server> --enumerate u
3)	When the wpscan process is done, it will list all the users it found. In my case, the admin user, and two test users I created for the purpose of this exercise.

<img src="User Enumeration.gif" alt="User Enumeration">
Once this is complete, it is likely that it would be followed up with another command.
•	wpscan –url <URL or IP address of server> -passwords <path to passwords.txt>
Now that they can get ahold of users with ease, they can run a list of passwords against each user to see if they can log in as a privileged user.

<h2>**Stored XSS via Comment Editing**</h2>
1.	Log into WordPress as an administrator, open a page, and write a new comment.
  
2.	The comment authorizes a few html tags and attributes, allowing the potential for XSS scripting to occur if it’s not sanitized properly.
  
3.	As admin, I entered the comment "a href=”yahoo.com” onmouseover=alert(“xss”)", stylized appropriately in html
  
4.	When anyone hovers over the link, the script will be executed. 

<img src="Commment XSS.gif" alt="Comment XSS">
  
<h2>**CRSF Press This DoS**</h2>
This one was rather fun albeit convoluted.
  
1.	Research the Press-This button. It acts as a quick link to publish a page, and can be done so from the browser’s bookmarks bar.
  <img src="Press This.gif" alt="Press-This gif 1">
  
2.	Created a new Ubuntu Linux Virtual Machine “evil-server” on VirtualBox 
  
3.	Installed the apache httpd service on evil-server.
  
  i.	Used sudo apt install apache2 for the install.
  
  ii.	Ensured the new http server worked.
  
4.	Navigated to /var/www/html
  
  i.	Created a new text file called foo.txt
  
  ii.	Used the fallocate command increase the size of the foo.txt to almost 10GB
  <img src="Fallocate.gif" alt="Press-This gif 2">
  
  iii.	Created a new html file called dos.html
  
5.	In the dos.html file, insert the command img src="http://192.168.33.10/wp-admin/press-this.php?u=http://192.168.10.82/foo.txt&url-scan-submit=Scan&a=b", stylized correctly in html, many times. This will force the press-this.php file on the WordPress server to retrieve foo.txt as an image from the evil server many times.
  <img src="dos.gif" alt="Press-This gif 3">
  
6.	On WordPress, created a page that has a link to 192.168.10.82/dos.html
  
7.	As an admin, click the bad link to evil-server/dos.html
  
8.	Attempt to open another page to the WordPress server. It cannot open because it is dossed.
<img src="dos attack.gif" alt="Press-This gif 4">
