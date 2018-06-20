[https://www.rsyslog.com/](https://www.rsyslog.com/)

[https://github.com/mthenw/frontail](https://github.com/mthenw/frontail)

All other containers are configured to send their log entries to this rsylog 'server'. This means all log entries (webserver requests entries, php errors, etc) are 
centralized in a unique place.

Frontail, a NodeJS application, is then used to stream that log in real time and provide some basic filtering.

![Frontail](frontail.png)