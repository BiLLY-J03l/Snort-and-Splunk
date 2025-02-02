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
## Create an account on Splunk website and install the Universal Forwarder

    sudo su
    wget -O splunkforwarder-9.4.0-6b4ebe426ca6-linux-amd64.deb "https://download.splunk.com/products/universalforwarder/releases/9.4.0/linux/splunkforwarder-9.4.0-6b4ebe426ca6-linux-amd64.deb"
    mv splunkforwarder-9.4.0-6b4ebe426ca6-linux-amd64.deb /opt
    dpkg -i splunkforwarder-9.4.0-6b4ebe426ca6-linux-amd64.deb
----------------------------------------------------------
## Accept Splunk Licence
  
    /opt/splunkforwarder/bin/splunk start

  ![image](https://github.com/user-attachments/assets/fedbbef5-edc9-41ec-936d-2fa3ee762a1a)
   
the username : password --> admin : adminadmin
    ![image](https://github.com/user-attachments/assets/701ea81e-4d86-4e0b-ad18-bb1cf2269fdf)

-------------------------------------------------------
