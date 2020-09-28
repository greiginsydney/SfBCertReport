The following script will query for every Skype for Business / Lync server in the environment which is a Registrar, EDGE, OWAS and PSTN Gateway and will retrive the following information on the certificates exists:

    Friendly Name
    Issuer
    Thumbprint
    Subject Name
    Issue Date
    Expiration Date
    Expires In (Days) 

Script Features:

    The script pulls the information from every server by query the Local Machine container to an HTML report file
    The script support Lync Certificates assignment awareness, meaning it only pull the assigned certificates from registrars (Front End & EDGE)
    The script query for every front end server in the pool which is based on Lync or Skype for Business version
    Certificates which are about to expired in the next 30 days will be colored in Red
    The script can also be configured to send email as well as being a scheduled task in order to be notified on a weekly/monthly basis.
    Support for EDGE servers Certificates retrieval
    Support Skype for Business Server 2015 environment
    The script include parameters which allow you to retrive certificates from FE, EDGE and OWAS all together or one at a time
    Connectivity tests for servers in Pool
    The sciprt pulls PSTN Gateway certificates information 

Version Control:

    0.1 - August-7-2014 - Initial Version for connecting Internal Lync Servers
    0.2 - August-8-2014 - With the help of Anthony Caragol, the script is now pulls information on every FE and using PSRemoting
    0.3 - August-8-2014 - Retrieves Information based on Lync assigned certificates
    0.45 - May-26-2015 - SfB Support, retrieves Information from EDGE Servers configured in the topology and adding Parameters Support
    0.46 - May-27-2015 - Improving connectivity test and OWAS display parameters
    0.47 - September-12-2015 - Fixed SYNOPSIS description
    0.48 - May 2016 - With the amazing help of Amanda Debler, she were able to insert a few more tests for pulling PSTN Gateway certs as well
    0.50 - July 2016 - ADded the option to work with a pre-loaded EDGE enrypted password file in order to scheduled the script to run autoamticlly  

Prerequisites:

Disclaimer: Please note that making the modification provided below and running the script is at your own risk.

In order to retrieve the Certificates information from the EDGE servers we need to use PSRemoting and Windows Remote Management for acccess.

This requires two major modifications:

1) On the Front End servers - Enabling TrustedHosts configurations:

Set-Item WSMan:\localhost\Client\TrustedHosts -Value "*" -Force

2) On the EDGE servers - Enabling HTTP Compatibility Listener for Remote access:

Set-Item WSMan:\localhost\Service\EnableCompatibilityHttpListener -Value True

Once enabled, you need to make sure port 80 is enabled from the computer where the script run to the EDGE internal IP.

Another options is to open the default PSRemoting Port as well (5895) and make sure to change the Parameter in the script ($PSRemoteConnectionPort). 

To view existing listeners, you can use the following command:winrm enumerate winrm/config/listener
Script Usage:

1) Retrieving all Lync Front End Pools Certificates information

.\SfBCertReport-v0.50.ps1

2) Retrieving all Lync Front End Pool Certificates information in addition to the EDGE Servers and OWAS Servers

.\SfBCertReport-v0.50.ps1 -EdgeCertificates -OWASCertificates

3) Retrieving all Lync Front End Pool Certificates information in addition to the EDGE Servers

.\SfBCertReport-v0.50.ps1 -EdgeCertificates

4) Retrieving all Lync Front End Pool Certificates information in addition to the OWAS Servers

.\SfBCertReport-v0.50.ps1 -OWASCertificates

5) Retrieving a spesific Front End Pool Certificates information

.\SfBCertReport-v0.50.ps1 -FEPool <Name of the FE Pool>

6) Retrieving PSTN Gateways Certificates information

.\SfBCertReport-v0.50.ps1 -PSTNGatewayCertificates

7) Retrieving EDGE Certificates information and read the EDGE administrator password from Encrypted file

.\SfBCertReport-v0.50.ps1 -EdgeCertificates -ReadEDGECredsFromFile

8) Retrieving environment certificates information

.\SfBCertReport-v0.50.ps1 -FEPool <Name of the FE Pool> -EdgeCertificates -ReadEDGECredsFromFile -OWASCertificates -PSTNGatewayCertificates


 

Output:
(snazzy image goes here)

Verified on the following platforms
Windows 10 	Yes
Windows Server 2012 	Yes
Windows Server 2012 R2 	No
Windows Server 2008 R2 	Yes
Windows Server 2008 	Yes
Windows Server 2003 	No
Windows Server 2016 	No
Windows 8 	No
Windows 7 	No
Windows Vista 	No
Windows XP 	No
Windows 2000 	No 
 
