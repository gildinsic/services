# services
systemd services


The initial goal of these processes was to *visualize* at once the rtt of a large number of (public) IP
It's been tested to monitor ~ 10 000 IP at a time

The IP are organized as /24 prefixes on a one page HTML application
The idea is to see minute by minute the evoloution for each IP and spot abnormal behaviors

Another idea was to expose the /24 based on the id of client-side certificates
For example in a multi "tenant/team" organisation sharing some prefixes

1 ping every 1s and circular graph

ping probes are ok 
tcp  probes 80/443 are not ok with bare nodejs library

Notice !! this is a tool to monitor *your own IP*


This is a work in progress  - recent code quick/dirty no var. tests

Some modules are not published or anonymzed for confidentiality reasons
Configuration is kept separated a much as possible


There is no code to log the probes in redis
It can be writtent easily by subscribing to the probe results
log ping could be done using redis persistence or influxdb time series db

A good idea to be coded would be a replay feature to see how the rtt evolve under increasing load



Link : good words on logging
https://blog.risingstack.com/node-js-logging-tutorial/


todo    add uuid to trace a specific IP across processes for distributed log session for debug

redis	used mainly for pubsub between processes
	multiple services producing/consuming redis events

influxdb (could be a good option to be tested for ping series)

services
	alert.mail	   alerting via email provider or SMTP (to be adapted as you want)
	alert.sms	   alerting via sms (to be adapted as you want)

	proxy		   (not public - two domains)
	pulse		   reporting/status (not public)
        
        pingwee		   the one page visualization of /24 ping probes (not yet public - to be anonymized)
	
        probe.ping	   echo req/reply/errors (detect changes and graph rtt)
	probe.tcp          test socket connect 80/443 (detect changes and graph rtt)
	probe.traceroute   to check /24 routes (and detect changes / routers)


Rem:    the MTR program is probably the best tool for traceroute probes
	there is a free API on something like "hackertarget"

