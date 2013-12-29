ddns
====

Self hosted Dynamic DNS


DNS Server side installation :
install any http server into your DNS server, 
such as thttpd or apache, or else.
Just make sure it supports bash cgi-bin
Configure your http server to support your URL to access your cgi-bin folder.
Copy "announce" script into your cgi-bin folder
Ensure the script is at least protected with http authentication.

add your new hostname and IP address (A Record) on your DNS configuration
reload your DNS server & start your http server.

Add this entry into your cronjob :
-*/18 * * * *   root  test -f /tmp/ddns && ( /etc/init.d/named reload; rm /tmp/ddns )
which will reload your DNS configuration each 18 minutes whenever changes occur
You can use any other intervals.

You pretty much done on server side.


DDNS Client side installation :

You can run following script at your server which has dynamically assigned IP address.
It will update your host name automatically.

Credentials stated in $USER:$PASSWORD for example : halims:mypassword
/usr/bin/curl -u $CREDENTIALS http://$DDNS_SERVER_HOST:$DDNS_SERVER_PORT/cgi-bin/announce?$CHANGED_HOSTNAME > /dev/null

you can choose to run this in timely manner by cronjob, 
or run this script once the host up the internet facing interface.




