# Snort-and-Splunk
Configuring Snort and Splunk as a SIEM solution on Linux

- What we will do?

 - Use Snort for implementing IDS rules.
 
 - Use Splunk Forwarder to forward the logs to our splunk server.
 
 - Use Splunk Enterprise to listen for the forwarded logs and alerts.
 
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

  - ![image](https://github.com/user-attachments/assets/35a621e3-0afa-4e98-9a49-3589204afb10)

- the username : password --> admin : adminadmin 
  - ![image](https://github.com/user-attachments/assets/62802e8c-8975-4b0e-804c-848bf0d63582)

----------------------------------------------------------
## Accept SplunkForwarder Licence and configure it to forward logs to the splunk instance on port 9997

    /opt/splunkforwarder/bin/splunk add forward-server localhost:9997
- ![image](https://github.com/user-attachments/assets/e876c0b3-246c-44dc-bb2a-59e10207e3d2)

- verify the configuration.
  - ![image](https://github.com/user-attachments/assets/639de289-1b06-4b07-8bbc-4a44fe58bda0)



  
   
the username : password --> admin : adminadmin
  

-------------------------------------------------------
## Open Browser and navigate to the host with port 8000

  ![image](https://github.com/user-attachments/assets/c13219cf-d7a4-432e-9f86-8b8fed44e4b8)
  ![image](https://github.com/user-attachments/assets/97ce9d1e-cf80-477c-8f89-cc15539f5946)

### configure receving on port 9997
![image](https://github.com/user-attachments/assets/45918f14-6cef-4947-940e-4ef9800110c8)
![image](https://github.com/user-attachments/assets/af230d20-47da-49e7-b77e-a08336cde572)
![image](https://github.com/user-attachments/assets/a5c3ec1f-77e8-4238-9120-4ac92d443ec9)

------------------------------------------------------------
## Add Snort. Navigate to Apps>Find more Apps> Search for ‘Snort’> Install Snort Alert for Splunk.

![image](https://github.com/user-attachments/assets/a92fcd08-35fe-4b0b-a426-27a59ec34e25)

------------------------------------------------------------
## Now for Snort Rules configurations

    sudo su
    vim /etc/snort/rules/local.rules
   
![image](https://github.com/user-attachments/assets/15d555fe-106e-4507-bc78-8985dfc13e0d)

-the file is blank by default. Let's add some rules to it.

![image](https://github.com/user-attachments/assets/8b7be5a0-4e9f-4a59-8fe5-2e670773e56e)

------------------------------------------------------------
## Continuing on SplunkForwarder

    /opt/splunkforwarder/bin/splunk add monitor /var/log/snort

 ![image](https://github.com/user-attachments/assets/3f9147bb-58e6-4f3b-8d77-d1d560dcc8d5)

    vim /opt/splunkforwarder/etc/apps/search/local/inputs.conf 
![image](https://github.com/user-attachments/assets/ec8695d5-1c49-4119-85a8-712e920edc4c)

- This file needs further configuration as follows

  - ![image](https://github.com/user-attachments/assets/6c3aab82-8451-461f-8278-ea03c6236022)



------------------------------------------------------------------
## Restart Splunk

    /opt/splunk/bin/splunk restart
    /opt/splunkforwarder/bin/splunk restart
------------------------------------------------------------------
## Final POV

- ![image](https://github.com/user-attachments/assets/0e64563e-9fc3-41c3-a714-e9cfc0327ebc)


- to test snort rules:

      snort -i enp0s3 -l /var/log/snort -c /etc/snort/snort.conf -A full
