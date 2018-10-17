### Dump1090-Daily-Aircraft-Report

Aggregates Dump1090-mutability messages to a daily report then emails and/or writes log-file and/or writes to MySql database

![Alt text](screen.png?raw=true "Sample Report")


  
**=> do the needed settings at top of ac_counter.php - then place the script e.g. in /home/pi/ and follow below instructions**

**starting with raspbian jessie or stretch install with dump1090-mutability:**

    sudo apt-get update

    install sendmail (only needed for email option):
    sudo apt-get install sendmail

    php install - raspbian jessie only:
    sudo apt-get install php5-common php5-cgi php5-mysql php5-sqlite php5-curl php5

    php install - raspbian stretch only:
    sudo apt-get install php7.0-common php7.0-cgi php7.0-mysql php7.0-sqlite php7.0-curl php7.0


**setup script system service:**

    sudo chmod 755 /home/pi/ac_counter.php
    sudo nano /etc/systemd/system/ac_counter.service

-> in nano insert the following lines

    [Unit]
    Description=ac_counter.php
    
    [Service]
    ExecStart=/home/pi/ac_counter.php
    Restart=always
    RestartSec=10
    StandardOutput=null
    StandardError=null
    
    [Install]
    WantedBy=multi-user.target

save and exit nano ctrl+x -> ctrl+y -> enter

    sudo chmod 644 /etc/systemd/system/ac_counter.service
    sudo systemctl enable ac_counter.service
    sudo systemctl start ac_counter.service
    sudo systemctl status ac_counter.service
    

