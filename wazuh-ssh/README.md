\#  Detecting SSH Brute-Force Attacks Using Wazuh



This project demonstrates how to detect SSH brute-force attempts using \*\*Wazuh\*\*, an open-source SIEM and XDR platform.  

The setup involves \*\*two Kali Linux machines\*\*:



\- \*\*Kali Machine 1:\*\* Wazuh Server + Dashboard  

\- \*\*Kali Machine 2:\*\* SSH client used to generate brute-force attempts  



The project includes examining predefined Wazuh rules, verifying SSH service status, creating a custom local rule, simulating brute-force activity, and analyzing triggered alerts.



---



\## Repository Structure



├── screenshots/

│   ├── wazuh-dashboard.png

│   ├── predefined-rule.png

│   ├── sshd-status.png

│   ├── local-rule.png

│   ├── triggered-alert.png

└── README.md



---



\## Project Objectives



\- Understand how Wazuh detects SSH login failures  

\- Analyze predefined SSH rules in Wazuh  

\- Simulate real SSH brute-force behavior  

\- Create a custom Wazuh rule using `local\_rules.xml`  

\- Trigger alerts and analyze them in the Wazuh dashboard  

\- Document the entire workflow for SOC analyst learning  



---



\## NOTE: This documentation does not cover the installation or initial setup of Wazuh.

&nbsp;        For installation and setup instructions, please refer to the official Wazuh                 

&nbsp;        documentation https://documentation.wazuh.com

---



\## Step 1: Trigger SSH failed authentication alerts



On Kali Machine 2:



Verify SSHD service is running:



!\[Verify SSHD](./screenshots/sshd\_status.png)



On Kali Machine 1:



&nbsp;``hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://<wazuh-server-ip>`` 

&nbsp;                 

Analyze the alerts: 



!\[Command](./screenshots/alerts\_command.png)



!\[Alerts](./screenshots/alerts.png)



---



\## Step 2: Analyze Predefined Rules



On Kali Machine 1:



&nbsp;``sudo cat /var/ossec/ruleset/rules/0010-sshd\_rules.xml``



Analyzed Rules:



!\[Predefined Rules](./screenshots/2501,2502.png)

!\[Predefined Rules](./screenshots/5758.png)

!\[Predefined Rules](./screenshots/5760.png)

!\[Predefined Rules](./screenshots/40111.png)

&nbsp;

---



\## Step 3: Create Wazuh Custom Rules



On Kali Machine 1: 

&nbsp;

&nbsp;``sudo nano /var/ossec/etc/rules/local\_rules.xml``



!\[Custom Rule](./screenshots/local\_rule.png)



---



\## Step 4: Restart and Test 





Now return to the Wazuh dashboard:



\- Go to \*\*Security Events\*\*  

\- Filter by your custom rule ID  

\- Confirm that the event is now detected and labeled with your custom description  



!\[Triggered Custom Rule](./screenshots/custom\_rule\_triggered.png)



---



\## End of Documentation





&nbsp;









