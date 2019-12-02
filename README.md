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
