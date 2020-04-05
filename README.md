                                                      Sorry Shaktiman!


	Loop.py - Code to make CPU utilization 100%:- 

	#!/usr/bin/env python3
	var =1
	while var>=1:
		print var*123
 	        var= var+2

	Useful Commands:-
	wget domain 2>&1 |grep Location:
	curl -v -L domain 2>&1 | egrep "^> (Host:|GET)"
	curl -Lv speevr.com/labs
	curl -Lv speevr.com/onepass -o /dev/null
	
	We'll use the following cURL command and options to get each step of our redirects.
	curl -s -L -D - http://test.chrislatta.org/myredirect.html -o /dev/null -w '%{url_effective}'


	To Check if an server is listening at port x
	nc -vz 13.52.160.194 x



--------------curl command curl -IvkL amol-biotech.com------entire flow of redirection----
		dig  edns-client-sub.net TXT to check if EDNS is enabled or not
		
sudo tcpdump -i en0 -n "port 8080" to get live packet capture

----------------------------------------------------------------------------------------------------
-->  curl -Ivk -w "\n\nTime Taken For Name Look-up: %{time_namelookup} \nTime Taken Establishing TCP Connection : %{time_connect} \nTime Taken For Appconnect: %{time_appconnect} \nTime Taken For Pre-Transfer:  %{time_pretransfer} \nTime Taken For First Byte Transfer : %{time_starttransfer} \nTime Taken For Redirect:  %{time_redirect}  \nTotal Time: %{time_total} \n +++++++++END++++++++++ \n" -o /dev/null https://URL;
Output:-
---------
lookup:        0.004181
connect:       0.005370
appconnect:    0.000000
pretransfer:   0.005394
redirect:      0.000000
starttransfer: 0.012130
total:         0.012172

----------------------------------------------------------------------------------------------------
--><h3>nslookup -debug whiteshadow.me. </h3>

Output:-
--------
Server:		172.31.0.2
Address:	172.31.0.2#53

------------
    QUESTIONS:
	whiteshadow.me, type = A, class = IN
    ANSWERS:
    ->  whiteshadow.me
	internet address = 192.30.252.154
	ttl = 60
    ->  whiteshadow.me
	internet address = 192.30.252.153
	ttl = 60
    AUTHORITY RECORDS:
    ADDITIONAL RECORDS:
------------
Non-authoritative answer:
Name:	whiteshadow.me
Address: 192.30.252.154
Name:	whiteshadow.me
Address: 192.30.252.153
------------
    QUESTIONS:
	whiteshadow.me, type = AAAA, class = IN
    ANSWERS:
    AUTHORITY RECORDS:
    ->  whiteshadow.me
	origin = dns1.registrar-servers.com
	mail addr = hostmaster.registrar-servers.com
	serial = 1578810829
	refresh = 3600
	retry = 1801
	expire = 604800
	minimum = 3601
	ttl = 60
    ADDITIONAL RECORDS:
------------



sudo tcpdump -ni any port 53 -w <FILENAME>.pcap to take packet capture
























NGINX - Managing SSL Certificates Using OpenSSL
Introduction

sudo su -

Create a Certificate Authority Private Key and Certificate

Create a directory to store our certificates:

mkdir -p /etc/nginx/certificates

Now let's get into it:

cd /etc/nginx/certificates

Generate a private key for the CA:

openssl genrsa 2048 > ca-key.pem

Generate the X509 certificate for the CA. For this step, just hit Enter at all of the prompts and use the default answers:

openssl req -new -x509 -nodes -days 365000 \
      -key ca-key.pem -out ca-cert.pem

Now if we run ls -la, we'll see those two new files listed.
Create a Private Key for the NGINX Server

Generate a private key and create a certificate request for the NGINX server:

openssl req -newkey rsa:2048 -days 365000 \
      -nodes -keyout server-key.pem -out server-req.pem

Accepting the default answers to these questions is fine, except for the Common Name. Fill something in, like TEST USER.

Process the key to remove the passphrase:

openssl rsa -in server-key.pem -out server-key.pem

We should see the following: writing RSA key
Create a Self-Signed Certificate for the NGINX Server

Generate a self-signed X509 certificate for the NGINX server:

openssl x509 -req -in server-req.pem -days 365000 \
      -CA ca-cert.pem -CAkey ca-key.pem -set_serial 01 \
      -out server-cert.pem

We now have self-signed X509 certificates for the NGINX server in the /etc/nginx/certificates directory. Run another ls -la to be sure.

We need to allow the nginx user access to the certificates. Add read permission for group and other:

chmod 644 *

Verify the Self-Signed Certificate for the NGINX Server

Let's use the openssl verify command to verify that the X509 certificate was correctly generated:

openssl verify -CAfile ca-cert.pem server-cert.pem

We should see the following: server-cert.pem: OK



<h2>Working with OpenSSL and Httpd</h2>


The virtual host should be accessible at shop.example.com:443 on the host webnode. The virtual host should operate over SSL using a 2048-bit self-signed private key. The key should be encrypted using AES128 and stored in /etc/pki/tls/private/httpdkey.pem on the webserver host using the passphrase httpd. The self-signed certificate should be stored in the file /etc/pki/tls/certs/httpdcert.pem on the webserver host.

You will need to allow HTTPS traffic through the OS-level firewall on port 443. This may be completed by running the following commands on the web server host:

sudo firewall-cmd --add-service=https --permanent
sudo firewall-cmd --reload

Once the virtual host and firewall access have been configured, verify that your configuration works by using the openssl s_client command. Output the secure connection information to /home/cloud_user/httpd_output on the host workstation.








Install mod_ssl on the Host webserver

    Log in to the webserver host.

    ssh webserver

    Escalate privileges to root.

    sudo su -

    Install mod_ssl.

    yum install -y mod_ssl

Generate and Sign a Private Key

    Change to the /tls/ directory.

    cd /etc/pki/tls/

    Create a new encrypted private key.

    openssl genrsa -aes128 -out private/httpdkey.pem

    Enter httpd at the next two passphrase prompts.
    Generate a self-signed certificate using the encrypted private key.

    openssl req -new -x509 -key private/httpdkey.pem -out certs/httpdcert.pem -days 365

    Enter httpd at the passphrase prompt.
    At the next prompt, enter the following information:
        Country Name: US
        State or Province Name: Texas
        Locality Name: Dallas
        Organization Name: Example Corp
        Common Name: shop.example.com
        Email Address: webmaster@example.com

Configure the Default Apache Virtual Host

    Edit /etc/httpd/conf.d/ssl.conf.

    vim /etc/httpd/conf.d/ssl.conf

    Type /Virtual to search for the SSH Virtual Host Context section.
    At the end of the <VirtualHost _default_:443> section, add the following on a new line:

    ServerName shop.example.com:443

    Type /SSLCert to search for the Server Certificate section.
    Locate the line SSLCertificateFile /etc/pki/tls/certs/localhost.crt, and change it to the following:

    SSLCertificateFile /etc/pki/tls/certs/httpdcert.pem

    Locate the line SSLCertificateKeyFile /etc/pki/tls/private/localhost.key, and change it to the following:

    SSLCertificateKeyFile /etc/pki/tls/private/httpdkey.pem

    Press Esc, then type :wq to exit the vim text editor.
    Restart the Apache httpd server.

    systemctl restart httpd

    Enter httpd at the passphrase prompt.
    Open port 443 on the OS firewall.

    firewall-cmd --add-service=https --permanent

    Reload the firewall.

    firewall-cmd --reload

Verify the Configuration

    Press Ctrl + D twice to log out of webserver and return to workstation.
    Verify that the configuration is working properly.

    openssl s_client -connect shop.example.com:443

    Press Ctrl + C to return to the command prompt.
    Write the s_client output to a file.

    openssl s_client -connect shop.example.com:443 > /home/cloud_user/httpd_output

    List the contents of the file to verify that the certificate information is there.

    cat /home/cloud_user/httpd_output


