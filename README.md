# Using-a-DISA-STIG-Scan-Template

I will demonstrate how to set up and use a DISA STIG scan template with vulnerabilities placed by me on the VM.

<h2>Requirements for this Lab</h2>
<br />

- <b> Azure </b>
- <b> Windows 10 Pro VM </b> 
- <b> Tenable.IO </b>

<h2>Walkthrough</h2>

<p align="center">
After creating my virtual machine on Azure, I will now begin the walkthrough on using scan templates to scan a Windows 10 VM.

<h2> 1. First, I will log onto the VM and disable the firewall. </h2>

<img src="https://i.imgur.com/mAutKKn.png" height="80%" width="80%" alt="Disable Firewall on VM"/>
<br />

To open up Windows Defender Firewall, type in the search bar the command:
>wf.msc
<br />

> Make sure Domain Profile, Private Profile, and Public Profile are all disabled.
<br />

<h2> 2. Now I'm going to set up the admin account, and set the password to "password with no expiration date. I will then enable the guest account and make them an administrator. </h2>

First, what I am going to do is go into computer management on the VM and create a user and place them within the administrator group and give them the password, "password", and make sure it never expires.
<br />

<img src="https://i.imgur.com/M9wlyHU.png" height="80%" width="80%" alt="admin creation"/>
<br />

I am also going to activate the guest account and make them a member of the admin group.

<img src="https://i.imgur.com/JIMqgi6.png" height="80%" width="80%" alt="admin creation"/>
<br />

> Enabling the account. 
 
<img src="https://i.imgur.com/PhRxJhS.png" height="80%" width="80%" alt="admin creation"/>
<br />

> Adding to the admin group.

<h3> When I run the scan templates on the VM, these issues should pop up since they violate DISA guidelines. </h3>
<br />

<h2> 3. I am now going to log into Tenable.io so I can create and run a custom advanced network scan template on the VM. </h2>


* Select Create a scan template
* Let the base be an advanced scan

Basic (Make sure all of these are checked)
* Never send credentials in the clear
* Do not use NTLMv1 authentication
* Start the Remote Registry service during the scan

Discovery 
* You ping the remote host
* Use fast network discovery
* Turn on TCP in Network Port Scanners.

Assessments,
* Check, Perform thorough tests
* Uncheck Only use credentials provided by the user in Brute Force.

Now I'm going to add the credentials of the REGULAR account I made.

After that, in compliance, I will search for DISA Windows 11 STIG

> Doing this allows the scan to look for the things that are asked within the parameters of the scan, like Password length, password complexity, etc.

<h3> Now the Scan template should show up in user-defined scans when creating a new scan. </h3>

<img src="https://i.imgur.com/B5MpphF.png" height="80%" width="80%" alt="scan template creation"/>
<br />

> As you can see, my "GOUB_STIG_DISA_Win11" Scan template is right there and ready to go.

All I have to do now is name my scan and provide the IP address.

<h3> I am going now to going to run the scan and wait for the results. </h3>
<br /> 

<h3> And here are the scan results !</h3>



Please note the Scan duration of 53 minutes & that over 11 vulnerabilities were found.

* 1 Critical
* 4 High
* 4 Medium
* 2 Low

<h3> Here are the DISA STIG Audit Results, with over 148 failures, 14 warnings, and 97 passed. I will include the failures of the vulnerabilities we set up in the VM earlier. </h3> 

We Should See issues with the password setups and the guest account. 

<img src="https://i.imgur.com/eieGaA6.png" height="80%" width="80%" alt="aduit results"/>
<br />

> Here are password failures, including WN11-00-000090, which states that Accounts must be configured to require password expiration.


<img src="https://i.imgur.com/wtpgclO.png" height="80%" width="80%" alt="aduit results"/>
<br />

> Here is a firewall failure, WN11-00-000135 - A host-based firewall must be installed and enabled on the system.

<img src="https://i.imgur.com/f3zbeEI.png" height="80%" width="80%" alt="aduit results"/>
<br />

> Here are vulnerabilities by asset, which basically shows the assets with the most vulnerabilities on them.

<img src="https://i.imgur.com/CJ2xXsx.png" height="80%" width="80%" alt="aduit results"/>
<br />

> Here are recommendations that can be done for certain vulnerabilities, and how many vulnerabilities per recommendation are solved 

<h1> All done. This was a complete custom advanced scan on tenable.io, which was compliant with DISA STIG on Windows 11 Machines. I will also include a copy of the entire scan results above. </h1> 

