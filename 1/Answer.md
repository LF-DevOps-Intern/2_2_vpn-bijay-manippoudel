> Setup a VPN server in one vm. You can use openvpn for this purpose.

+ You should have two network interface one for wan and another for lan. You should setup vpn server which listens on wan interface and provides lan interfaces subnets ip address to the client which connects using openvpn client.

    - We can see the available interface using  ifconfig command.
    - Reference Picture (network_lan_wan_interface.png)

+ Openvpn installation and easy-rsa installation.   
    - sudo yum install openvpn
    - Installed the old version of easy rsa using wget.
    - wget https://github.com/OpenVPN/easy-rsa-old/archive/2.3.3.tar.gz
    - Reference Picture(easy_rsa_installation.png)

+ You should create certificates files for both server and client to connect to server and export client certificates to the client vm.
    - Created dir in openvpn folder for easy-rsa
        - cmd : mkdir -p /etc/openvpn/easy-rsa/keys
    - Copied the easy rsa version 2 in the open vpn folfer 
    - Reference Picture(easy_rsa_installation.png)

    - For Certificate Generation:
        - Reference Picture (certificate_generate_1.png)
        - Reference Picture (certificate_generate_2.png)
        - Reference Picture (certificate_keys_client_server.png)

+ For routing the packets.
    ```
    # To add openvpn service permanently to Trusted zone.
    sudo firewall-cmd --zone=trusted --add-service openvpn --permanent

    # To get the list of all the trusted zones.
    sudo firewall-cmd --list-services --zone=trusted

    # Masquerade Permanently
    sudo firewall-cmd --permanent --add-masquerade

    # Adding the routing rule. (Reference Picture vpn_masquerade.png)
    sudo firewall-cmd --permanent --direct --passthrough ipv4 -t nat -A POSTROUTING -s 10.8.0.0/24 -o 192.168.1.67 -j MASQUERADE



    # NOTE: We should always reload firewall after any changes to the firewall setting using:
    sudo firewall-cmd --reload

    # Reload the openvpn server after the server.conf file is changed.
    systemctl restart openvpn-server@server.service

    # Renamed the openssl file
    cp /etc/openvpn/easy-rsa/openssl-1.0.0.cnf /etc/openvpn/easy-rsa/openssl.cnf
    
    #Static key generation (Encryption Key)

    sudo openvpn --genkey --secret /etc/openvpn/user.tlsauth

    ```



