ddns
====

Self hosted Dynamic DNS


DNS Server side installation : <br>
install any http server into your DNS server, 
such as thttpd or apache, or else.<br>
Just make sure it supports bash cgi-bin. <br>
Configure your http server to support your URL to access your cgi-bin folder.<br>
Copy "announce" script into your cgi-bin folder.<br>
Ensure the script is at least protected with http authentication.<br>
<br>
add your new hostname and IP address (A Record) on your DNS configuration, <br>
reload your DNS server & start your http server.

Add this entry into your cronjob : <br>
-*/18 * * * *   root  test -f /tmp/ddns && ( /etc/init.d/named reload; rm /tmp/ddns ) <br>
which will reload your DNS configuration each 18 minutes whenever changes occur<br>
You can use any other intervals.
<br>
You pretty much done on server side.


DDNS Client side installation : <br>

You can run following script at your server which has dynamically assigned IP address.<br>

Credentials stated in $USER:$PASSWORD for example : halims:mypassword <br>
/usr/bin/curl -u $CREDENTIALS http://$DDNS_SERVER_HOST:$DDNS_SERVER_PORT/cgi-bin/announce?$CHANGED_HOSTNAME > /dev/null<br>

you can choose to run this in timely manner by cronjob, 
or run this script once the host up the internet facing interface.




