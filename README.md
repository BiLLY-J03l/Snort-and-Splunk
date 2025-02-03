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
## Accept SplunkForwarder Licence

    /opt/splunkforwarder/bin/splunk start

  ![image](https://github.com/user-attachments/assets/fedbbef5-edc9-41ec-936d-2fa3ee762a1a)
   
the username : password --> admin : adminadmin
    ![image](https://github.com/user-attachments/assets/701ea81e-4d86-4e0b-ad18-bb1cf2269fdf)

-------------------------------------------------------
