> Research on IDS/IPS. There are many applications that provide IDS/IPS service. Find one of the opensource service and install it on the VM1 you created previously. Try to set up IDS which block some of the known vulnerabilities signature.

# Snort is one of the Opensource Intrusion Prevention Detection System that I have configured in my CentOs server.



+  Firstly I checked out the snort.org and followed the installation through

    https://snort.org/#get-started 

    - Check the dependency for Snort or DAQ by:
        - rpm -qa | grep gcc 
        - rpm -qa | grep flex
        - rpm -qa | grep bison
        - rpm -qa | grep tcpdump
        - rpm -qa | grep libdnet-devel
    - For the dependency not available I checked out rpmfind.net site and installed the required dependency.

+ Then I downloaded the daq using wget and extracted it and installed.
    - wget https://snort.org/downloads/snort/daq-2.0.7.tar.gz
    - tar xvzf daq-2.0.7.tar.gz
    - ./configure && make && sudo make install

+ After successfully installing daq I install snort using
    - yum install https://snort.org/downloads/snort/snort-2.9.18.1-1.centos8.x86_64.rpm

    - Reference Picture (snort_installation_yum.png)
    - For version check Reference Picture (snort_version_check.png)
    - After Snort was successfully installed. I make some configuration file changes to snort.conf file in /etc/snort/ dir.
        + I changed the ipvar HOME_NET value to my LAN IP address class(192.168.1./24).
        + Then I updated the path for Whitelist and Blacklist rules along with uncomming the line so that the local.rules file in /etc/snort/rules dir can be executed bt snort for rules.

        + I updated the the rule to check ICMP .
            - alert icmp 192.168.1.68 any -> 192.168.1.67  any (msg:"ICMP Ping Passed"; sid:10000001; rev:001;)
        
        + After changing the conf file and adding the rule I tested my configuration files.
            - Reference Document : Configuration_Testing_Snort.md
    
    - After that I ran the Snort Configuration live in the console.
        + Reference Picture(snort_running_in_console.png)
    + Then I pinged the server from the client.
        + Reference Picture(ping_snort_from_client.png)
    + THe ping was successfully detected in the client.
        + Reference Picture (ping_detected_in_server.png)


