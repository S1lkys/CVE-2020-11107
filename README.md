# CVE-2020-11107
This is a writeup for CVE-2020-11107 I've found.


An issue was discovered in XAMPP before 7.2.29, 7.3.x before 7.3.16 , and 7.4.x before 7.4.4 on Windows.
An unprivileged user can change a .exe configuration in xampp-contol.ini for all users (including admins) to enable arbitrary command execution.

All this can be done through xampps control-panel.


XAMPP allows an unprivileged User to access and modify its editor and browser configuration. The default value is notepad.exe
The default value can be changed to set a bat file as the editor or browser. After saving the configuration, it changed for every user which can access the control panel. 
If an attacker sets the notepad value to a malicious .exe file or .bat file it gets executed after another user tries to open the log files via the control panel. This can result in grating a normal user admin privileges or worse.


A step by step PoC can be found below:
1. Default values of XAMPP‘s config file.
![alt text](https://github.com/S1lkys/CVE-2020-11107/blob/master/Step1-Default%20Configuration.PNG )


2. Normal user which can access the control panel.
![alt text](https://github.com/S1lkys/CVE-2020-11107/blob/master/Step2-Normal%20User%20Silky.PNG)


3. Changing the notepad.exe file as User Silky to a malicious file.
![alt text](https://github.com/S1lkys/CVE-2020-11107/blob/master/Step3-Changing%20the%20editor.PNG)


4. Config of Administrator got changed as well.
![alt text](https://github.com/S1lkys/CVE-2020-11107/blob/master/Step4-Administrator%20File%20changed.PNG)


5. Administrator tries to view a log file.
![alt text](https://github.com/S1lkys/CVE-2020-11107/blob/master/Step5-Admin%20tries%20to%20access%20log%20file.PNG)


6. Code gets executed and grants User Silky Admin rights.
![alt text](https://github.com/S1lkys/CVE-2020-11107/blob/master/Step6-%20Silky%20got%20Admin%20Privs.PNG)





# References: 
1. https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2020-11107
2. https://www.apachefriends.org/blog/new_xampp_20200401.html
3. https://nvd.nist.gov/vuln/detail/CVE-2020-11107
