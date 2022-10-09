---
title: Nginx Web Server
description: Basic information about Nginx and how to secure it for a Production environment
published: true
date: 2022-10-09T23:05:47.296Z
tags: nginx, webserver, config
editor: markdown
dateCreated: 2022-10-09T23:05:47.296Z
---

# Securing Nginx

<br>

### Default Config Files and Locations

**Server Configuration File**
`/etc/nginx/nginx.conf`

**Default Webroot Directory**
`/var/www/html`

**Log File Location**
`/var/log/nginx`

>When making changes to nginx's configuration, you can test the syntax by running `nginx -t`. 
{.is-info}

<br>

### Restrictive IPTables Based Firewall
The script below configures a firewall to block everything except incoming TCP Port 80, incoming ICMP ping requests, outgoing NTP port 123 requests, and outgoing SMTP TCP port 25 requests.

````bash
#!/bin/bash
IPT="/sbin/iptables"
 
#### IPS ######
# Get server public ip
SERVER_IP=$(ifconfig eth0 | grep 'inet addr:' | awk -F'inet addr:' '{ print $2}' | awk '{ print $1}')
LB1_IP="204.54.1.1"
LB2_IP="204.54.1.2"
 
# Do some smart logic so that we can use damm script on LB2 too
OTHER_LB=""
SERVER_IP=""
[[ "$SERVER_IP" == "$LB1_IP" ]] && OTHER_LB="$LB2_IP" || OTHER_LB="$LB1_IP"
[[ "$OTHER_LB" == "$LB2_IP" ]] && OPP_LB="$LB1_IP" || OPP_LB="$LB2_IP"
 
### IPs ###
PUB_SSH_ONLY="122.xx.yy.zz/29"
 
#### FILES #####
BLOCKED_IP_TDB=/root/.fw/blocked.ip.txt
SPOOFIP="127.0.0.0/8 192.168.0.0/16 172.16.0.0/12 10.0.0.0/8 169.254.0.0/16 0.0.0.0/8 240.0.0.0/4 255.255.255.255/32 168.254.0.0/16 224.0.0.0/4 240.0.0.0/5 248.0.0.0/5 192.0.2.0/24"
BADIPS=$( [[ -f ${BLOCKED_IP_TDB} ]] && grep -E -v "^#|^$" ${BLOCKED_IP_TDB})
 
### Interfaces ###
PUB_IF="eth0"   # public interface
LO_IF="lo"      # loopback
VPN_IF="eth1"   # vpn / private net
 
### start firewall ###
echo "Setting LB1 $(hostname) Firewall..."
 
# DROP and close everything
$IPT -P INPUT DROP
$IPT -P OUTPUT DROP
$IPT -P FORWARD DROP
 
# Unlimited lo access
$IPT -A INPUT -i ${LO_IF} -j ACCEPT
$IPT -A OUTPUT -o ${LO_IF} -j ACCEPT
 
# Unlimited vpn / pnet access
$IPT -A INPUT -i ${VPN_IF} -j ACCEPT
$IPT -A OUTPUT -o ${VPN_IF} -j ACCEPT
 
# Drop sync
$IPT -A INPUT -i ${PUB_IF} -p tcp ! --syn -m state --state NEW -j DROP
 
# Drop Fragments
$IPT -A INPUT -i ${PUB_IF} -f -j DROP
 
$IPT  -A INPUT -i ${PUB_IF} -p tcp --tcp-flags ALL FIN,URG,PSH -j DROP
$IPT  -A INPUT -i ${PUB_IF} -p tcp --tcp-flags ALL ALL -j DROP
 
# Drop NULL packets
$IPT  -A INPUT -i ${PUB_IF} -p tcp --tcp-flags ALL NONE -m limit --limit 5/m --limit-burst 7 -j LOG --log-prefix " NULL Packets "
$IPT  -A INPUT -i ${PUB_IF} -p tcp --tcp-flags ALL NONE -j DROP
 
$IPT  -A INPUT -i ${PUB_IF} -p tcp --tcp-flags SYN,RST SYN,RST -j DROP
 
# Drop XMAS
$IPT  -A INPUT -i ${PUB_IF} -p tcp --tcp-flags SYN,FIN SYN,FIN -m limit --limit 5/m --limit-burst 7 -j LOG --log-prefix " XMAS Packets "
$IPT  -A INPUT -i ${PUB_IF} -p tcp --tcp-flags SYN,FIN SYN,FIN -j DROP
 
# Drop FIN packet scans
$IPT  -A INPUT -i ${PUB_IF} -p tcp --tcp-flags FIN,ACK FIN -m limit --limit 5/m --limit-burst 7 -j LOG --log-prefix " Fin Packets Scan "
$IPT  -A INPUT -i ${PUB_IF} -p tcp --tcp-flags FIN,ACK FIN -j DROP
 
$IPT  -A INPUT -i ${PUB_IF} -p tcp --tcp-flags ALL SYN,RST,ACK,FIN,URG -j DROP
 
# Log and get rid of broadcast / multicast and invalid
$IPT  -A INPUT -i ${PUB_IF} -m pkttype --pkt-type broadcast -j LOG --log-prefix " Broadcast "
$IPT  -A INPUT -i ${PUB_IF} -m pkttype --pkt-type broadcast -j DROP
 
$IPT  -A INPUT -i ${PUB_IF} -m pkttype --pkt-type multicast -j LOG --log-prefix " Multicast "
$IPT  -A INPUT -i ${PUB_IF} -m pkttype --pkt-type multicast -j DROP
 
$IPT  -A INPUT -i ${PUB_IF} -m state --state INVALID -j LOG --log-prefix " Invalid "
$IPT  -A INPUT -i ${PUB_IF} -m state --state INVALID -j DROP
 
# Log and block spoofed ips
$IPT -N spooflist
for ipblock in $SPOOFIP
do
         $IPT -A spooflist -i ${PUB_IF} -s $ipblock -j LOG --log-prefix " SPOOF List Block "
         $IPT -A spooflist -i ${PUB_IF} -s $ipblock -j DROP
done
$IPT -I INPUT -j spooflist
$IPT -I OUTPUT -j spooflist
$IPT -I FORWARD -j spooflist
 
# Allow ssh only from selected public ips
for ip in ${PUB_SSH_ONLY}
do
        $IPT -A INPUT -i ${PUB_IF} -s ${ip} -p tcp -d ${SERVER_IP} --destination-port 22 -j ACCEPT
        $IPT -A OUTPUT -o ${PUB_IF} -d ${ip} -p tcp -s ${SERVER_IP} --sport 22 -j ACCEPT
done
 
# allow incoming ICMP ping pong stuff
$IPT -A INPUT -i ${PUB_IF} -p icmp --icmp-type 8 -s 0/0 -m state --state NEW,ESTABLISHED,RELATED -m limit --limit 30/sec  -j ACCEPT
$IPT -A OUTPUT -o ${PUB_IF} -p icmp --icmp-type 0 -d 0/0 -m state --state ESTABLISHED,RELATED -j ACCEPT
 
# allow incoming HTTP port 80
$IPT -A INPUT -i ${PUB_IF} -p tcp -s 0/0 --sport 1024:65535 --dport 80 -m state --state NEW,ESTABLISHED -j ACCEPT
$IPT -A OUTPUT -o ${PUB_IF} -p tcp --sport 80 -d 0/0 --dport 1024:65535 -m state --state ESTABLISHED -j ACCEPT
 
 
# allow outgoing ntp
$IPT -A OUTPUT -o ${PUB_IF} -p udp --dport 123 -m state --state NEW,ESTABLISHED -j ACCEPT
$IPT -A INPUT -i ${PUB_IF} -p udp --sport 123 -m state --state ESTABLISHED -j ACCEPT
 
# allow outgoing smtp
$IPT -A OUTPUT -o ${PUB_IF} -p tcp --dport 25 -m state --state NEW,ESTABLISHED -j ACCEPT
$IPT -A INPUT -i ${PUB_IF} -p tcp --sport 25 -m state --state ESTABLISHED -j ACCEPT
 
### add your other rules here ####
 
#######################
# drop and log everything else
$IPT -A INPUT -m limit --limit 5/m --limit-burst 7 -j LOG --log-prefix " DEFAULT DROP "
$IPT -A INPUT -j DROP
 
exit 0
````

### Stop Image Hotlinking
> Add these lines within your Domain server block
{.is-info}


````bash
location /images/ {
  valid_referers none blocked www.example.com example.com;
   if ($invalid_referer) {
     return   403;
   }
}
````

### Nginx & PHP Security Tips
> You can change these options by opening your php.ini file located at `/etc/php/*.*/fpm/php.ini`
{.is-info}


````ini
# Disallow dangerous functions
disable_functions = phpinfo, system, mail, exec
 
## Try to limit resources  ##
 
# Maximum execution time of each script, in seconds
max_execution_time = 30
 
# Maximum amount of time each script may spend parsing request data
max_input_time = 60
 
# Maximum amount of memory a script may consume (8MB)
memory_limit = 8M
 
# Maximum size of POST data that PHP will accept.
post_max_size = 8M
 
# Whether to allow HTTP file uploads.
file_uploads = Off
 
# Maximum allowed size for uploaded files.
upload_max_filesize = 2M
 
# Do not expose PHP error messages to external users
display_errors = Off
 
# Turn on safe mode
safe_mode = On
 
# Only allow access to executables in isolated directory
safe_mode_exec_dir = php-required-executables-path
 
# Limit external access to PHP environment
safe_mode_allowed_env_vars = PHP_
 
# Restrict PHP information leakage
expose_php = Off
 
# Log all errors
log_errors = On
 
# Do not register globals for input data
register_globals = Off
 
# Minimize allowable PHP post size
post_max_size = 1K
 
# Ensure PHP redirects appropriately
cgi.force_redirect = 0
 
# Disallow uploading unless necessary
file_uploads = Off
 
# Enable SQL safe mode
sql.safe_mode = On
 
# Avoid Opening remote files
allow_url_fopen = Off
````

## Nginx.conf
> The following snippets can be added to the nginx.conf file to enable globally, or they can be added to individual Virtualhost files.
{.is-info}



## avoid clickjacking

````nginx
add_header X-Frame-Options SAMEORIGIN;
````

## Disable content-type sniffing

````nginx
add_header X-Content-Type-Options nosniff;
````

## Enable XSS Filter

````nginx
add_header X-XSS-Protection "1; mode=block";
````