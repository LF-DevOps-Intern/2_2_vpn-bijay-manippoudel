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

