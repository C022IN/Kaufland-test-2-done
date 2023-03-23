# Kaufland-test-2-done

Kaufland Test Challenge 2

Steps taken:
1.	Access the service on http://localhost:5001
I found that access to the website is forbidden using an authentication-based access. 
 
I checked the installation and found that some of the permissions to access the files might be restricted.

 
2.	 Performing enumeration
I performed Nikto tests on the local host using the exposed port 5001. This uncovered a potentially malicious file /.htpasswd which contains authorization information
 
Other than that, some of the vulnerabilities were also exposed showing a high probability of the following:
•	X-Frame-Options header not present
•	X-Content-Type-Options header is not set
•	/.htpasswd: Contains authorization information.

3.	Uncovering/ Scanning
Performed a bypass scan using a tool to uncover paths that return a 200 response. I also checked the same using Burp Suite. I uncovered some of the paths as shown below
 
Checking the /.htpasswd link prompted for a file download. This file contains login credentials to access the application.
 

4.	Gaining Access
Upon getting the authentication credentials, I still encountered a 403 Error. I performed more bypass checks using potentially relevant wordlists. I finally received a 401 Error on /login Path.
 
Using the link gave me a login pop up window:

 
I used the logins found earlier and successfully accessed the site 😊.
 
 
 



Other Tests performed in this project.
1.	Permissions
Changed permissions to files and directories in this project to allow Read, Write & Execute.
 
 

2.	Configured the nginx.conf file
Changed configurations in the nginx.conf file to allow all for directory level access.
 
3.	Check for directories and secrets.
Performed a wide range of tests to trace the path with a 200 response.
 
 



4.	Check HTTP Methods
Checked for possibility of getting 200 responses from some HTTP Methods
 
Also changed the HTTP Version to detect any possible vulnerabilities 


Done Well
1.	Trace,put,delete Not Allowed
 


















Vulnerabilities exposed

 
X-Frame-Options header not present
Impact: This is an indication that the website is vulnerable to a clickjacking attacks. The use of this header will ensure that the site cannot be embedded in other sites.
Remediation: Set the security header X-Frame-Options to indicate to the browser not to render any iframe. this can used by sending a response header X-Frame-Options: DENY or X-Frame-Options: SAMEORIGIN if you want to use iframes but only for pages that are in the same origin as your page.

X-Content-Type-Options header is not set
Impact: The server did not return a correct 'X-Content-Type-Options' header, which means that this website could be at risk of a Cross-Site Scripting (XSS) attack.
Remediation: Configure your web server to include an 'X-Content-Type-Options' header with a value of 'nosniff

/.htpasswd: Contains authorization information (Broken Access Control).
Impact: Bypassing access control checks by modifying the URL (parameter tampering or force browsing), internal application state, or the HTML page, or by using an attack tool modifying API requests.
Remediation: Disable web server directory listing and ensure file metadata (e.g., .git) and backup files are not present within web roots. Also ensure proper encryption of passwords in configuration files
 


Tools used:
•	Bypass 403
•	Nikto
•	Nmap NSE
•	Burp Suite
