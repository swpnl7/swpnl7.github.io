                                                      Hey!


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
-->  curl -L --output /dev/null --silent --show-error --write-out 'lookup:        %{time_namelookup}\nconnect:       %{time_connect}\nappconnect:    %{time_appconnect}\npretransfer:   %{time_pretransfer}\nredirect:      %{time_redirect}\nstarttransfer: %{time_starttransfer}\ntotal:         %{time_total}\n' 'whiteshadow.me'

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
