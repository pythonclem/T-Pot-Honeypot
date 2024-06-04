# Setting Up A Honeypot 🍯

**`How I Used T-Pot and Splunk To Create And Monitor Attacks`**
   </br>

## 📜 The Why
Going into this project I had four main goals: getting comfortable with SSH and Linux, getting comfortable with configuring a firewall, subnets, and general aspects of cloud networking, getting comfortable with Azure, and getting first hand experience in setting up a honeypot and monitoring it with Splunk. 
  
   </br>

## 📜 The What
HoneyPot is a T-pot installation on an Azure VM, with a main Splunk instance installed on a VM in another network, and a Splunk forwarder configured on the HoneyPot machine. T-pot is a set of honeypots made available by T-Mobile with dozens of honeypots installed to allow monitoring of scanning and attacks. 

   </br>

## 📜 The How
First, I had to set up my networks in Azure, including the security groups. I spun up the recommended VMs to install both Splunk and T-pot. The T-pot installation went smoothly, but I couldn’t access the web interface. After a while troubleshooting, I realized I had misconfigured the security group and erred on the strict side - which is the side I generally prefer to err on. I then set up Splunk on the other machine, and finished by configuring the forwarder on both machines. 

   </br>

## 🚨 My First Incident
At one point I was looking at the log stream and saw an alert from Suricata in all caps: TROJAN HORSE DETECTED ON NETWORK. Because this was a honeypot VM, I expected many logs to tell me something bad tried to happen. But I didn't expect this one. 

My first action was to isolate the machine and block all incoming and outgoing traffic, and since I only had one VM on the network, I figured completely isolating the machine will give me time to investigate properly, in case something happened. 

I opened the log in Splunk and started investigating. I saw it was coming from Suricata and that it flagged a data transfer, and assumed that data was being exfiltrated from my machine. As I went over the details, I saw the IP that the data was being sent to - and it seemed familiar. It didn’t take more than a minute for me to realize that the data transfer was simply the Splunk forwarder sending logs to the main Splunk instance I had set up on another network. Thankfully, there was no trojan horse on my network - there was just a need to fine tune the monitoring to avoid future heart attacks. 

   </br>

## 📜 The Challenges
As I’ve been learning more and more about security, I’ve generally thrown myself into projects without necessarily understanding the true scope of what I’m about to build. This project was originally a lot more complex, with ELK stack configuration and many other interacting VMs. Halfway through, I adjusted the project to be more in line with what I felt like I had a chance to pull off. I’d rather try to do too much than not enough, but sometimes adjustments are needed.

   </br>

## 📜 The Lessons
From cloud computing and VMs to configuring Splunk and living in Linux for a few days, this project got me the furthest into infosec than I’ve ever been before. I learned the importance of proper configuration (both for security groups and monitoring), and had my first live incident response which allowed me to instinctively apply the frameworks I’ve only had theoretical knowledge of. 10/10 would set this up again.


