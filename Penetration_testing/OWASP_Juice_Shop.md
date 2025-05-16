# OWASP JUICE SHOP - PEN TEST

## Introduction
This assessment aims to discover and identify vulnerabilities on The Juice Shop’s website and recommend methods to remediate them.

## Objective
The objective of this report is to provide an analysis of the possible vulnerabilities and flaws discovered on the Juice Shop website as well as proposed measures that could be implemented to resolve these issues. This piece of work equally helps us to figure out the effectiveness of the security measures already put in place to make sure they can withstand possible attacks from potential threat actors. It’s worth mentioning that the discovered loopholes have been classified and eventual recommendations have been formulated to ease understanding and enable the decision-makers to easily come up with a response plan.
 
## Requirements
The penetration test focused on Juice Shop version 15.3.0 deployed within a Docker container hosted on a Linux VM. The Kali OS comes with a number of built-in tools. The main one used for this assessment was Burp Suite Community Edition. This is a powerful tool used in penetration tests for web applications. The assessment spanned both front-end and back-end components and extended over a one-month period. Notably, the testing team operated without administrative or normal credentials and instead simulated an authenticated user scenario to assess security controls. The primary aims of this penetration test were to identify vulnerabilities, evaluate existing controls, and provide guidance. Throughout the testing process, efforts were made to avoid disruptions to legitimate users.

## Execution Environment
To properly perform the penetration testing, it is primordial to have a proper environment
  - Firstly, I had to pull the website using the command docker pull bkimminich/juice-shop. 
  - Then, it was typed the command docker run --rm -p 3000:3000 bkimminich/juice-shop was typed. This command enables us to run the website on the local host at the address 127.0.0.1 using port 3000. <br/>

<img src="https://github.com/user-attachments/assets/0cc6fa06-17d7-4036-971a-f1c823e31be5" width="500"></br>
Figure 1. Website running on localhost. </br></br>

After running the website, the architecture looked like this: </br>

<img src="https://github.com/user-attachments/assets/cfd59fbe-0860-4419-aded-4839e5895631" width="500"></br>
Figure 2. Testing Environment. </br></br>

## High-Level Summary 
It has identified a total of 9 vulnerabilities within the scope, categorized by severity in the table below.</br>
<img  src="https://github.com/user-attachments/assets/6d012adb-6d9b-4548-8062-5eebb6b000dc" width="500"></br>
Table 1. Vulnerabilities Classification.</br></br>

The Juice Shop website environment was developed using the JavaScript programming language, Angular, Node.JS Framework, and SQLite Database. The environment contains numerous vulnerabilities, including some serious security flaws such as unencrypted passwords and an easily accessible Admin Account, which makes it possible for threat actors to steal data and perform system takeovers.
To perfectly assess the task handed to us, two frameworks were used to classify the discovered vulnerabilities: OWASP (Open Worldwide Application Security Project) and NIST SP800-53 (National Institute of Standards and Technology). These are two international frameworks that serve as guidelines to ensure our different systems, networks and applications are robust against attacks. The OWASP Top 10 serves as a standard awareness document aimed at various web developers and web application security that classifies the most common vulnerabilities known to web applications. It is a widespread agreement on the most significant security risks inherent in web applications. NIST SP 800-53 offers a collection of controls that systems and organizations can use to handle the risks associated with information security and privacy.
Highly important files having sensitive information about the business and clients are easily accessible and visible, putting The Juice Shop at great risk of compliance violation and potentially subjecting it to large fines and/or loss of business reputation.
Among all the vulnerabilities discovered, the most critical ones are SQL Injection and Sensitive Data Exposure. Through these vulnerabilities, an attacker could potentially gain unauthorized access, view sensitive data, and even manipulate the information on The Juice Shop website. To ensure the confidentiality, integrity, and availability of data, it is imperative that security remediations be implemented, as described in the recommendations section.</br>

## Risk Rating
The severity rating helps to determine which of the vulnerabilities may have the greatest impact on the functioning and reputation of the company or cause the greatest losses if exploited by an attacker. It’s worth mentioning that the risk ratings attributed to the vulnerabilities are personal judgments based on theoretical and practical experience. These ratings are:
 - Critical: These are vulnerabilities that could be actively exploited in real-world situations, and they may allow remote exploitation by external attackers. A significant impact on the business could be caused by these security flaws, making it necessary for immediate attention in the form of a workaround and/or temporary protection.
 - High: These are vulnerabilities that may potentially have serious impacts on the enterprise. These vulnerabilities may require a change in the security systems.
 - Medium: These are vulnerabilities that could potentially contribute indirectly to a more significant incident or be exploited directly to a limited extent in terms of availability and/or impact. This category of vulnerability is not likely to result in a significant compromise on its own; however, a substantial danger can be posed when combined with others.
 - Low: These are vulnerabilities which may present little or no risk directly but may provide valuable information on the structure or functioning of the system to possible attackers.</br></br>

The table below gives an overview of the discovered vulnerabilities and their severity.</br>
<img src="https://github.com/user-attachments/assets/3ab4fd77-88fb-456c-9b10-eba21ea55761" width="500"></br>
Table 2. Rating of Findings.</br></br>

## Report - Methodologies 
### SQL Injection

During a web application's design, it is important to properly define the type of input that should be accepted within a given entry area. If this is not done, it opens a loophole in the application which can be exploited by possible threat actors. One of such attacks that could be performed is the Structured Query Language (SQL) Injection. SQL injection is a vulnerability in web security that enables an attacker to manipulate the queries executed by an application on its database. The table below gives us the references from OWASP and NIST when it comes to SQL Injection.</br>
<img src="https://github.com/user-attachments/assets/ab427413-56ea-4613-9cab-c8ca80312524" width="500"></br>
Table 3: SQL Injection References.</br></br>

It has been discovered that the login page of the Juice Shop Website is susceptible to SQL Injection. Hence, by entering the query ‘ or 1=1-- as username and putting any password, I was able to access the admin account of the web application. As such, it was possible to read some valuable information from the database and perform administrative operations. The screenshot below shows how this attack was performed.</br>
<img src="https://github.com/user-attachments/assets/279cd0e4-9a77-46b6-ad49-d15938a6c65e" width="500"></br>
Figure 3: SQL Injection performed.</br></br>
This command will log us into the admin account as shown in the screenshot below:</br>
<img src="https://github.com/user-attachments/assets/046d4a76-a783-4082-ac08-90762fe6f424" width="500"></br>
Figure 4: Access granted to the admin account.</br></br>

#### Recommendations
 - Juice Shop should use parameterized queries when interacting with the database backend. A parameterized query is a method whereby the SQL query is differentiated from the user input values. This implies that the input values will no longer be seen as executable code but as simple parameters. Nowadays, parametrized queries are known to be one of the most effective ways to avoid SQL Injection attacks.
 - Incorporate features into the application to conduct integrity checks on received data. If the data does not align with the anticipated format, it should be rejected.
 - Also, it is strongly recommended that the developers make use of the SQL Injection Cheat Sheet using the URL https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html. This will help them get acquainted with the different measures to be taken to avoid SQL Injection.</br></br>
 
### Authorization Bypass

An authorization bypass happens when someone can get around the planned security measures and gain unauthorized access or privileges for specific functions. In simpler terms, it is a security weakness that allows an attacker access to resources or does things without the right permission or proper authentication. The main problem is that the application doesn't validate input properly. When a web app takes input from a user and uses it to get data or grant access, it is crucial for the app to confirm that the user is allowed to do that specific action. Authorization bypass is recognized and classified in the following table. During the penetration tests, two categories of authorization bypass were identified: Coupon fraud and User Role.

#### Coupon Fraud
The coupon fraud is recognized as authorization bypass, and it is classified in the following table.</br>
<img src="https://github.com/user-attachments/assets/e8f3736d-275f-4778-b800-6cdfa101bea7" width="500"></br>
Table 4. Coupon Fraud classification.</br></br>

The ability to obtain a coupon from a chatbot simply by insisting on it indicates a lack of thorough testing before deploying the feature into production. This kind of flaw could potentially allow anyone to exploit the system and receive unauthorized discounts, posing a risk of financial loss for the organization.
To take advantage of this vulnerability, a person must log into their account and look for ‘Support Chat’ in the left menu.</br>

<img src="https://github.com/user-attachments/assets/d6156d0c-77d6-4c3c-9044-125b9278cf95" width="500"></br>
Figure 5: Accessing the account.</br></br>

<img src="https://github.com/user-attachments/assets/bf9f845a-7bf7-4e08-a1c8-841f2bd7412c" width="500"></br>
Figure 6: Looking for an online chat.</br></br>

Once on that webpage, the person must give a name and afterwards ask for a coupon.</br>
<img src="https://github.com/user-attachments/assets/4e88aab9-b629-4484-9418-3205bef3916a" width="500"></br>
Figure 7: Giving a name and asking for a coupon.</br></br>

<img src="https://github.com/user-attachments/assets/7f738281-2964-4233-a84c-c99c76bf46d1" width="500"></br>
Figure 8: Insisting on the request.</br></br>

<img src="https://github.com/user-attachments/assets/82eb7b9a-9e89-4f38-8e34-9862a8429570" width="500"></br>
Figure 9: Coupon obtained.</br></br>

As shown in the earlier screenshots, by insisting on the coupon, the chatbot gives a 10 % coupon without authorization from the CFO or the person in charge.
##### Recommendations 
 - Conduct a thorough test of the features that are going to be implemented before they are launched into production. This way, various vulnerabilities can be discovered and addressed on time.
 - The adoption of the Least Privilege Principle which involves assigning the minimum necessary permissions to users or systems for their tasks. By doing so, you ensure that users or systems can only perform actions essential to their roles or tasks, reducing the risk of unauthorized or unintended activities.

#### User Role
The user role is an important aspect of account management. These roles are often linked to an account and transmitted to the database during account creation. An attacker may capture these roles upon account creation and modify them to give privileges to the account being created. The account data in transit during creation is vulnerable to being captured if an attacker is present on the internal network. Therefore, encrypting all information sent over the network is a good practice. If the information is not encrypted and authentication mechanisms are not functioning correctly, sensitive information can be viewed and even manipulated, leading to unauthorized activities.</br> 

<img src="https://github.com/user-attachments/assets/c91e7b56-4f72-4c84-90e1-ac7061c65997" width="500"></br>
Table 4. User Role Classification.</br></br>

A proxy server must be used; in this case, the tool Burp Suite has its own browser by so it’s not necessary to edit the proxy configurations in a normal web browser. To exploit this vulnerability, the attacker must create a new user.</br>

<img src="https://github.com/user-attachments/assets/85851a10-c8ab-4be0-8c2e-09d38d86c810" width="500"></br>
Figure 10: Creation of a new account.</br></br>

<img src="https://github.com/user-attachments/assets/925c0593-0d7b-4aed-a7d4-adc079d9a5c3" width="500"></br>
Figure 11: Data captured.</br></br>

Once the Register button is clicked, Burp Suite intercepts all the data, allowing the attacker to view sensitive information such as email and password. This tool also aids in filtering all the requests sent to the database. The POST method is used to send all the information from the front end to the back end. Posteriorly, the feature of the Repeater has to be used to be able to see the response that the database showed.</br>

<img src="https://github.com/user-attachments/assets/11fd121d-381a-497a-a798-c2747b046d00" width="500"></br>
Figure 12: Request and Response.</br></br>


This information is crucial because the attacker could see two important attributes: status and role. Those attributes could be changed and added to the request field.</br>

<img src="https://github.com/user-attachments/assets/60c01993-9bc6-496e-9c79-b12c45daf3cc" width="500"></br>
Figure 13: Manipulation of the Request field.</br></br>

As is shown in the previous image, data was manipulated and a second request was made to the database, in that second request the email was changed, creating a second account, and the role was added, giving the Administrator access to the new account.

<img src="https://github.com/user-attachments/assets/271002b5-d650-4561-8386-5652fec644ba" width="500"></br>
Figure 14. Log in to the new account.</br></br>

<img src="https://github.com/user-attachments/assets/bc7c8f53-ec05-43d9-b857-ab02035d0ac1" width="500"></br>
Figure 15. Account profile.</br></br>

Data in transit was manipulated to gain Administrator privileges, this action may allow threat actors to perform any malicious activity.</br>

#### Recommendations 
- Use of encryption tools to encrypt the data during transmission using secure protocols such as TLS/SSL. This helps protect data integrity and confidentiality. This way, even if an attacker can see the data, the information will be unreadable.
- Inclusion of mechanisms in the application to perform data integrity checks upon receiving data. If the data doesn't match the expected format or values, it may indicate tampering, and further investigation will take place.
- Monitoring systems might be implemented to detect anomalies or suspicious activities during data transmission. Monitor logs and network traffic for signs of unauthorized changes.

### Capturing and manipulating data in transit
Stored data or in-transit data is highly valuable for organizations, threat actors can acquire sensitive information, modify the content, and potentially insert false information if the data is not correctly protected. This can lead to serious security breaches and compromise the confidentiality, integrity, and availability of the transmitted data. Among all the industry standards, capturing and manipulating data in transit is classified in the following table.</br>

<img src="https://github.com/user-attachments/assets/757c6750-6161-4577-bbc8-e7bc147f68ad" width="500"></br>
Table 5. Data exposure classification.</br></br>

To demonstrate this vulnerability, first, items were added to the basket. This action has been captured by Burp Suite before it reaches the database (the reason why we have basket content as 0) as shown in the screenshot below. </br>

<img src="https://github.com/user-attachments/assets/5abf7f6c-cb20-4d34-a79e-493763a2cc9c" width="500"></br>
Figure 16. Item added to the basket captured.</br></br>

It’s important to take note of the values of the “ProductId”, “BasketId” and “quantity”. As can be seen, the product with ID=1 was added to the basket in a quantity=1. The next step is to send these captured packets to the ‘Repeater’, where the aforementioned values shall be modified before being sent.</br>

<img src="https://github.com/user-attachments/assets/ba9d1424-d8be-47cd-94e1-222d5457037d" width="500"></br>
Figure 17. Modification of captured packets.</br></br>
 
In the previous image, it can be seen that productId, which has a value of 2 with a quantity of 5, was added to the basket and sent.
After this is done, it is noticed that the content of the basket has changed as shown below.</br>

<img src="https://github.com/user-attachments/assets/61aa90b6-9548-4d84-8809-54167a6dd14c" width="500"></br>
Figure 18. Products added to basket by attacker.</br></br>

Due to sensitive data exposure and undefined packet forwarding policies, I have been able to modify the content of a given basket. This can have severe repercussions, such as loss of trust from customers and reduced online shopping, thereby leading to heavy losses by the enterprise.</br>

#### Recommendations  
- Ensure the encryption of all transmitted data using protocols such as TLS (Transport Layer Security)
-  Avoid using outdated protocols such as FTP and SMTP for transporting sensitive data.

### Deficient Security Standards for Password Storage 
Encryption is a technique that involves converting transmitted data into an unreadable form such that only authorized users can access and understand it. This is done with the use of an encryption key. Unsecured communication channels are susceptible to potential interception and alteration.

<img src="https://github.com/user-attachments/assets/63d871f8-acfe-4f23-a448-93552e986aea" width="500"></br>
Table 4: References for Non-encrypted Password</br></br>

To check this out, the first step is to open the log-in interface. Then we have to turn on the Intercept option of Burp Suite. We move to the browser and input the credentials.</br>

<img src="https://github.com/user-attachments/assets/816b5a07-8ac4-4c67-ab77-fbbe9f7d81cb" width="500"></br>
Figure 19. Credentials filled.</br></br>

Burp Suite then captures the packets sent. Upon capturing, we noticed the credentials had been sent in plain text. This makes it possible for an intruder to view and take note of the credentials without having to unhash or decrypt them.</br>

<img src="https://github.com/user-attachments/assets/9ced2fe2-9330-4e9f-963d-4e8ecdca2718" width="500"></br>
Figure 20. Credentials are captured and displayed in plain text.</br></br>

#### Recommendations 
- Juice Shop should implement Transport Layer Security. This is a well-known protocol that encrypts information that is sent over the network using a 256-bit encryption cipher.
- Deploy resilient network security measures to safeguard data during transit. Security solutions such as firewalls and network access control play a crucial role in fortifying the networks involved in data transmission, defending against malware attacks, and preventing intrusions.

### Cross-Site Scripting Flaws
Cross-site scripting (XSS) is a security vulnerability that occurs when a website allows malicious code to be injected into the website. Attackers inject malicious scripts, typically coded in JavaScript, into the web page content. When unsuspecting users access the compromised page, these scripts execute in their browsers, allowing the attacker to hijack user sessions, steal sensitive data, or perform unauthorized actions on behalf of the user. </br>

#### DOM XSS (Document Object Model Cross-Site Scripting)
This is a special type of XSS which involves injecting malicious scripts that enable the user to manipulate the DOM. This flaw directly affects the Document Object Model on the user side. This may be caused by error handling, client-side rendering or dynamic content updates. Document Object Model (DOM)-based XSS modifies the hierarchical depiction of a web page's structure.</br>
Document Object Model is a web browser-provided programming interface, The DOM allows scripts to modify the content, layout, and style of online pages. It presents the document as an object structure that resembles a tree and that scripts can modify to change the way the page functions without requiring a full page reload.

<img src="https://github.com/user-attachments/assets/09a96550-c18a-4186-a22b-457538273bed" width="500"></br>
Table 5. References for XSS.</br></br>

To assess if the website is subject to this flaw, an HTML label was filled into an input space:
 h1 Test1 has been here h1

The screenshot below gives us the outcome of this HTML tag.

<img src="https://github.com/user-attachments/assets/d49cf82c-8bac-42f3-919d-e5439b9f8029" width="500"></br>
Figure 22. An HTML tag is embedded in the webpage.</br></br>

Another way of verifying this could be by inserting the script command <iframe src=”javascript:alert(‘Test’)”> into the input space.

<img src="https://github.com/user-attachments/assets/b137caa5-e759-4c32-8814-8cc1d7ed9298" width="500"></br>
Figure 23. JavaScript code is injected into the webpage.</br></br>

<img src="https://github.com/user-attachments/assets/e1f8cbf2-1bae-420e-9559-41f7e52d1fd3" width="500"></br>
Figure 24. JavaScript code is injected into the webpage.</br></br>

A strange behaviour in the application occurred when specific payloads were injected during testing. The program displayed unexpected script execution, suggesting that there may be a Document Object Model (DOM) vulnerability that may be used to execute malicious code (XSS).  

##### Recommendations
- Implement robust input validation and sanitization procedures on both client and server sides. Utilize relevant validation libraries or functions to ensure thorough cleaning of user inputs.
- Make sure to use secure output encoding libraries. Apply contextual output encoding, such as HTML-encoding data before insertion into HTML content, to enhance defense against malicious scripts.
- Conduct regular code reviews focusing on secure coding techniques. Equally emphasize training on input validation and output encoding to prevent potential security issues.

### Deficient Complexity in Password
Around the globe multiple users now access numerous Portal for various purposes, in today's time as people faces and get to know about many cyber-crimes so many organizations have improved, or we can say they have set up some conditions to set user account password to prevent users from frauds and easily access of account by hackers. Deficient complexity in a password refers to a situation where the password used is too simple or predictable. This could mean that the password is too short, does not include a mix of letters, numbers, and special characters, or is a commonly used or easily guessable password. Such passwords are easier for attackers to guess or crack using various methods, such as brute force attacks (where every possible combination is tried), dictionary attacks (where every word in the dictionary is tried), or by using lists of commonly used passwords.

<img src="https://github.com/user-attachments/assets/458aad50-6e1f-47e8-8ad0-81bb28beb64a" width="500"></br>
Figure 25. Password advice on the Juice Shop website.</br></br>

<img src="https://github.com/user-attachments/assets/27a82eee-1761-4883-ad0c-a6868a0acf3e" width="500"></br>
Figure 26. Registration Successful.</br></br>

<img src="https://github.com/user-attachments/assets/7901c63a-8fdb-4f10-9ffb-827fc80623bd" width="500"></br>
Figure 27. Registration with Simple password.</br></br>

It was found that while registering as a new user on the juice shop website, the person can select any password of their choice, even though the website mentions some characteristics for the password setup. Hence, the User can select a simple password such as 123456 when the website mentions some password advisory on the screen while registering.</br> 
The table below gives us the references OWASP and NIST when it comes to Password complexity.

<img src="https://github.com/user-attachments/assets/49069ff0-e1ee-4852-b651-4e14e188982f" width="500"></br>
Table 6. References for Password Policies.</br></br>

#### Recommendations
It is highly recommended that the password policy be enforced at the time of user registration. The system should not allow the registration process to be completed until a sufficiently complex password is entered. Also, implement both client-side and server-side validation. While client-side validation can provide immediate feedback to the user, server-side validation is crucial, as client-side validation can be bypassed. Apart from this, regularly audit and test the system to ensure that password policies are being enforced. This could involve penetration testing or the use of automated security scanners.

### Deficient Error Management
It has encountered a server error on the OWASP Juice Shop website. The error was a 500-server error, indicating an unexpected condition that prevented the server from fulfilling the request. The error message was ‘Unexpected path: /rest/qwertz’, suggesting an incorrect or unexpected request sent to the server.</br>

The error page reveals the crucial information that is meant to be protected, exposing information on the error, making it easier for an attacker to know the vulnerabilities of the system. Such information can be exploited by malicious users to attack the application. Therefore, proper error handling is important to prevent such information leakage and enhance the security of web applications.

<img src="https://github.com/user-attachments/assets/bb944337-906f-4593-9d2b-1b16ca203876" width="500"></br>
Figure 28. Redirecting to rest/qwertz.</br></br>

<img src="https://github.com/user-attachments/assets/fde42833-86f5-4722-a8c2-87d58a5b6e80" width="500"></br>
Figure 29. 500 error on OWASP Juice Shop website.</br></br>

This usually occurs when detailed internal error messages, such as stack traces, database dumps, and error codes, are displayed to the user. It’s recommended to handle errors in a way that provides a meaningful error message to the user and diagnostic information to the site maintainers, without revealing any useful information to potential attackers.</br>
Error: Unexpected path: /rest/wztp: This is the error message. It indicates that the application encountered an unexpected path (/rest/wztp).</br>

at Function.handle (/home/juice-shop/node_modules/express/lib/router/index.js:95): This line tells you that the error occurred in the handle function in the index.js file located in the /home/juice-shop/node_modules/express/lib/router/ directory. The error occurred at line 95 of this file.</br>

at router (/home/juice-shop/node_modules/express/lib/router/index: This line indicates that the error occurred in the router function in the index file located in the /home/juice-shop/node_modules/express/lib/router/ directory.</br>

The error message “Unexpected path: /rest/wztp” can provide valuable information to a potential attacker in several ways:
- Understanding Application Logic: The error message indicates that the application didn’t expect a request to the path “/rest/wztp”. This could suggest to an attacker that the application might have other, potentially vulnerable, paths that it does not expect.
- Information Gathering (Reconnaissance): The error message could be a part of the attacker’s information gathering phase, where they are trying to collect as much information about the system as possible before launching an attack.</br>

<img src="https://github.com/user-attachments/assets/63286711-ae0d-4511-80bc-98a993f2f2b7" width="500"></br>
Table 7. References for Improper Error Handling.</br></br>

#### Recommendations 
- Avoid Revealing Sensitive Information: Make sure that error messages and debugging information do not disclose sensitive information or system details1. This includes internal workings, database dumps, stack traces, and error codes.
- Implement Generic Error Messages: Good generic messages do not disclose sensitive information about the application like stack traces, database queries, or file paths. A good error message reveals just enough information to the user to know what's happening and how to proceed or resolve the issue without revealing sensitive or unnecessary details.
- Security Training and Awareness: Developers and stakeholders should be educated on the importance of protecting sensitive information from disclosure and sharing verbose error messages. 

### Access To the File Directory
It has been discovered that the OWASP Juice Shop website has an irregularity. Regular users can sneak a peek at the file directory via /ftp. Now, this directory is not just filled with any old files; it has some pretty important stuff, like details about orders and the company’s future plans. Normally, you wouldn’t want just anyone to be able to access this. But due to a server misconfiguration (a bit like forgetting to lock the door), users can. This is often called a Directory Listing Vulnerability or Directory Traversal.</br>

<img src="https://github.com/user-attachments/assets/b77ae671-8f64-4f4f-b2c6-14551bd0774b" width="500"></br>
Figure 30. /ftp file directory of the website.</br></br>

<img src="https://github.com/user-attachments/assets/36615e43-1587-4535-8e09-b3687ee79911" width="500"></br>
Figure 31. Access to directory file and downloaded successfully.</br></br>

Directory Listing Vulnerability is a security flaw that arises when a server’s settings are improperly configured, allowing users to view the contents of a directory in the absence of an index file. This could potentially reveal confidential files to any user who knows where to look. It’s a method that compromises confidentiality.
It particularly increases the exposure of sensitive files within the directory that are not intended to be accessible to users, such as temporary files and crash dumps.</br>
Directory listing is not inherently a vulnerability. It’s a feature of a web server that shows the contents of a directory when there’s no index file in a specific website directory. However, if this feature is left active in a production environment, it can make your server susceptible to disclosing information. It’s like leaving the library doors open with no librarian. Anyone who knows where to look could find and read information that you might not want to be public.</br>
Restricting access to important directories or files by adopting a need-to-know requirement for both the document and server root, and turning off features such as Automatic Directory Listings that could expose private files and provide information that could be utilized by an attacker when formulating or conducting an attack.</br>

<img src="https://github.com/user-attachments/assets/33ec9842-8506-4775-b419-96e88f7ddfd4" width="500"></br>
Table 8. References to File Directory policies.</br></br>

#### Recommendation
- It is highly recommended to set proper file and directory permissions. Sensitive files should not be stored in publicly accessible directories. Following this, Using Index File by this means ensuring that each directory has an index file (like index.html or index.php). When a user navigates to a directory, the web server will display the index file instead of a directory listing.
- Regularly audit your website for directory listing vulnerabilities. This can be done manually or with the help of automated tools. Undoubtedly, Education and training regarding cybersecurity and organizations should be willing to invest in cybersecurity mitigation to prevent companies from such attacks.
