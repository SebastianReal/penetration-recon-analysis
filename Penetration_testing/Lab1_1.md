# Laboratory - Reconnaissance and Gathering Information 

## Task 1
Choose any large public company or organization (except SLC) and use the reconnaissance techniques (various websites and tools, social media etc.)

## Development
The company that has been chosen is Capital One Bank, which uses the domain capitalone.com, primarily because of a cyber-attack that it has suffered in the past.

Reconnaissance:

Reconnaissance refers to the process of collecting information and intelligence about a specific target. In cybersecurity, the targets are commonly computer systems, networks, or specific groups of people. This constitutes the initial step taken by threat actors to gather information about the target, which can be done actively or passively.

Starting with the reconnaissance phase, the tool hunter.io makes gathering sensitive information much easier because the tool provides many results with only one search. Following the search of the domain.

<img src="https://github.com/user-attachments/assets/a6b47570-2059-442f-a0ab-b63073738003" width="500"><br>
Figure 1. Search on the hunter.io website. <br/><br/>


In the image above, it is notable that 685 corporate email accounts are exposed on the internet and may be easily found by third parties with no connections to the bank. Additionally, sometimes the search can reveal a person’s job, which is highly inconvenient from an information security perspective. 


The previous one was the first step when it comes to gathering information; now that names, positions, and emails are known, social media is the next step. Everybody these days has either social network accounts to share moments with close people or social media accounts for business/professional growth. However, this information can be seen by everybody and among those, there might be threat actors.

Below is an example of the information, such as social media webpages, public records, and phone numbers, that can be extracted with one search on the website peekyou.com about Capital One’s Vice President. 

<img src="https://github.com/user-attachments/assets/601b252f-9737-4524-aeeb-57b2fd3a202f" width="500"><br>
Figure 2. Results for Andrew Sherry, who lives in New York. <br/><br/>


<img src="https://github.com/user-attachments/assets/86eac0c9-2962-4c28-95fe-d52101af7bb0" width="500"><br>
Figure 3. Results for Andre Sherry's Facebook accounts. <br/><br/>


Sometimes, research through social media accounts is not fruitful, so other research could be done through business or professional social media accounts such as LinkedIn and Glassdoor, which are big companies with lots of information about people around the world. Below is an example of a search on LinkedIn about the selected target.

<img src="https://github.com/user-attachments/assets/e979ddb3-a00b-48a3-af22-0bc3af71e1b1" width="500"><br>
Figure 4. Andrew Sherry’s LinkedIn Profile. <br/><br/>


<img src="https://github.com/user-attachments/assets/6c9a90c4-2a97-4b41-9e2b-fbff5becf472" width="500"><br>
Figure 5. Andrew Sherry’s Activity and Job Experience. <br/><br/>


With the tools mentioned before, a threat actor could start planning a Reconnaissance attack by applying some techniques such as phishing for information, gathering victim organization information, searching open databases, and so on.


Having the personnel information alone is not enough to carry out a successful attack. It's crucial to gather information about the devices and technology used within the company. Therefore, companies should put significant effort into protecting that information. Below are some examples of the information that might be obtained by a threat actor with web tools such as builtwith.com, censys.io, and netcraft.com. 


Firstly, builtwith.com is an online tool that provides information about the technologies and software used by other websites on the internet. By doing a single search of a domain name, it provides a detailed report on the various technologies, frameworks, content management systems (CMS), analytics tools, and more that the domain is using.


<img src="https://github.com/user-attachments/assets/93682780-0a5a-4bed-9659-6001541b1d49" width="500"><br>
Figure 6. Information about capitalone.com. <br/><br/>


<img src="https://github.com/user-attachments/assets/41f3b3dc-eada-4db1-b311-a11dcffbc277" width="500"><br>
Figure 7. Load performance of capitalone.com. <br/><br/>


<img src="https://github.com/user-attachments/assets/58d4cf34-3f83-48ad-aefc-a86f44066386" width="500"><br>
Figure 8. The annual budget for the IT infrastructure of capitalone.com. <br/><br/>


Figures six (6), seven (7), and eight (8) provide more information about employees, the company’s hierarchy, addresses, employees' social media profiles, and more. Additionally, the search revealed sensitive information about the budget allocated for the IT department. All this information could potentially be considered a data breach since people from all around the world can access it, and the company is unaware of when an attack might occur.


Going deeper into technological details, websites like censys.io and netcraft.com provide enormous amounts of information about what software is running the applications, the IP addresses that the server is using, the server type (cloud or on-premises), the records of the web trackers, and so on. Below are some technical details obtained with those mentioned tools.

<img src="https://github.com/user-attachments/assets/d153c58c-e62c-46d1-a64c-6420c8772ef7" width="500"><br>
Figure 9. Network information of capitalone.com. <br/><br/>


<img src="https://github.com/user-attachments/assets/f7aeba89-bab5-4601-8df3-be9f5ab45a6d" width="500"><br>
Figure 10. Services, ports, and software used by capitalone.com. <br/><br/>


Figures nine (9) and ten (10) display information about the Background and Network. While the background information might not be useful for a threat actor, the network information, which includes ports and services, is highly valuable, as a threat actor can and will use this information to carry out an attack. Information such as IP addresses and Name servers is public, but if not well protected, they could become potential targets for a DoS attack or DDoS attack. This figure also illustrates geographical localization and network segmentation, which are crucial for a better understanding of how the network is configured. In addition to all the technical information, the email address of the DNS administrator is provided and could potentially be used for a phishing attack.


<img src="https://github.com/user-attachments/assets/ad7b678f-cf17-4304-8259-d1953fe04525" width="500"><br>
Figure 11. Site technology of capitalone.com. <br/><br/>


<img src="https://github.com/user-attachments/assets/c7698577-e21c-4fb0-9741-ac4ac04864d1" width="500"><br>
Figure 12. Hosts and Autonomous System of capitalone.com. <br/><br/>


<img src="https://github.com/user-attachments/assets/9131209c-d06f-42c2-9051-2a0f70b1fa79" width="500"><br>
Figure 13. Tool nslookup used with capitalone.com. <br/><br/>


Figures eleven (11), twelve (12), and thirteen (13) show more information about the technology used by the target system. Most of this information is public so everyone can perform the search, but that information combined with poor cybersecurity practices is all that a threat actor needs to perform a cyber-attack. 







