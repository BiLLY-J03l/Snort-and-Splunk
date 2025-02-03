# Snort-and-Splunk
Configuring Snort and Splunk as a SIEM solution on Linux

What we will do?

 -Use Snort for implementing IDS rules.
 
 -Use Splunk Forwarder to forward the logs to our splunk server.
 
 -Use Splunk Enterprise to listen for the forwarded logs and alerts.
 
--------------------------------------------------------

## Update the linux instance first

    sudo su
    apt update; apt full-upgrade -y; apt autoremove -y
    init 6
---------------------------------------------------------
## Install Snort

    sudo su
    apt install snort -y
----------------------------------------------------------
## Create an account on Splunk website and install the Universal Forwarder and Splunk Enterprise

    sudo su
    wget -O splunkforwarder-9.4.0-6b4ebe426ca6-linux-amd64.deb "https://download.splunk.com/products/universalforwarder/releases/9.4.0/linux/splunkforwarder-9.4.0-6b4ebe426ca6-linux-amd64.deb"
    wget -O splunk-9.4.0-6b4ebe426ca6-linux-amd64.deb "https://download.splunk.com/products/splunk/releases/9.4.0/linux/splunk-9.4.0-6b4ebe426ca6-linux-amd64.deb"
    mv splunkforwarder-9.4.0-6b4ebe426ca6-linux-amd64.deb /opt
    mv splunk-9.4.0-6b4ebe426ca6-linux-amd64.deb /opt
    dpkg -i splunkforwarder-9.4.0-6b4ebe426ca6-linux-amd64.deb
    dpkg -i splunk-9.4.0-6b4ebe426ca6-linux-amd64.deb
----------------------------------------------------------
## Accept Splunk Enterprise Licence

    /opt/splunk/bin/splunk start

   ![image](https://github.com/user-attachments/assets/35a621e3-0afa-4e98-9a49-3589204afb10)

the username : password --> admin : adminadmin
   ![image](https://github.com/user-attachments/assets/62802e8c-8975-4b0e-804c-848bf0d63582)

----------------------------------------------------------
## Accept SplunkForwarder Licence and configure it to forward logs to the splunk instance on port 9997

    /opt/splunkforwarder/bin/splunk add forward-server localhost:9997
  ![image](https://github.com/user-attachments/assets/b2d29daf-4ef8-4ce5-bb21-85468ed92928)

  
   
the username : password --> admin : adminadmin
  

-------------------------------------------------------
## Open Browser and navigate to the host with port 8000

  ![image](https://github.com/user-attachments/assets/c13219cf-d7a4-432e-9f86-8b8fed44e4b8)
  ![image](https://github.com/user-attachments/assets/97ce9d1e-cf80-477c-8f89-cc15539f5946)





