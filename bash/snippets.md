---
title: Collection of Random Bash Snippets
description: 
published: true
date: 2022-07-19T11:59:05.751Z
tags: bash, snippets
editor: markdown
dateCreated: 2022-07-05T06:37:33.445Z
---

# Check the SSH Log file for newly created Users

<br>

````bash
grep useradd /var/log/auth.log
````

<br>

# Echo Public IP Address using Curl

<br>

````bash
curl ifconfig.me.`  
````

<br>

# Print the currently installed PHP Version #

<br>

````bash
php -v | grep ^PHP | cut -d' ' -f2
````

<br>

# Exit Status One-Liner

<br>

````bash
[ $? -eq 0 ] && echo "SUCCESS" || echo "FAILED"  
````

<br>

# Fetch Geodata

<br>

````bash
curl "http://ip-api.com/line/?fields=query,city,region,country,zip,isp"
````

<br>

# Find files in current directory that have been modified in the last 24hrs

<br>

````bash
find . -maxdepth 1 -mtime -1
````

<br>

# Delete files older than 5 days


<br>

````bash
find /path/to/directory/ -mindepth 1 -mtime +5 -delete
````

<br>

# Fix Mysql Root User

<br>

````bash
UPDATE mysql.user SET Grant_priv = 'Y', Super_priv = 'Y' WHERE User = 'root';
````

<br>

# Generate Self Signed SSL

<br>

````bash
openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -days 10000 -nodes
````

<br>

# Print IP Address from Ifconfig Command

<br>

````bash
ifconfig | grep -Eo 'inet (addr:)?([0-9]*\.){3}[0-9]*' | grep -Eo '([0-9]*\.){3}[0-9]*' | grep -v '127.0.0.1'
````

<br>

# GREP IP Address from a File

<br>

````bash
grep -E -o "([0-9]{1,3}[\.]){3}[0-9]{1,3}"
````

<br>


# List Installed Packages

<br>

````bash
dpkg --l
````

<br>


# Search for Installed Package

<br>

````bash
dpkg --list | grep PACKAGE_NAME
````

<br>


# SSH-KEYGEN Non interactive

<br>

````bash
ssh-keygen -q -t rsa -N '' -f ~/.ssh/id_rsa <<<y >/dev/null 2>&1
````

<br>


# Remove Duplicate Lines from a file

<br>

````bash
awk '!seen[$0]++' FILENAME
````

<br>


# Create TAR Archive from .txt File

<br>

````bash
tar -czvf ARCHIVE_NAME.tar.gz -T DIRECTORY_LIST.txt
````

<br>


# List only Usernames from /etc/passwd File

<br>

````bash
cut -d: -f1 /etc/passwd
````

<br>


# Print the # of Lines in a file

<br>

````bash
wc -l FILENAME.txt | awk '{ print $1 }'
````

<br>


# Read a File Line by Line

<br>

````bash
while read -r line; do
// Commands here
done<INPUT_FILE.txt
````

<br>

# Mysql Secure Installation

<br>

````bash
mysql -u root -pPASSWORDHERE<< _EOQ_
SET PASSWORD FOR root@localhost = PASSWORD('ROOTPASSWORDHERE');
FLUSH PRIVILEGES;
DELETE FROM mysql.user WHERE User='';
DELETE FROM mysql.user WHERE User='root' AND Host NOT IN ('localhost', '127.0.0.1', '::1');
DROP DATABASE test;
DELETE FROM mysql.db WHERE Db='test' OR Db='test_%';
CREATE USER 'USERNAMEHERE'@'localhost' IDENTIFIED BY 'PASSWORDHERE';
GRANT ALL PRIVILEGES ON *.* TO 'USERNAMEHERE'@'localhost';
FLUSH PRIVILEGES;
_EOQ_
````

<br>

# Sed Commands to configure PHP.ini Files

<br>

````bash
sed -i 's/memory_limit = 128M/memory_limit = 512M/g' /etc/php/7.4/fpm/php.ini
sed -i 's/memory_limit = 128M/memory_limit = 512M/g' /etc/php/7.4/cli/php.ini
sed -i 's/memory_limit = 128M/memory_limit = 512M/g' /etc/php/7.4/apache2/php.ini
````
````bash
sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 100M/g' /etc/php/7.4/fpm/php.ini
sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 100M/g' /etc/php/7.4/cli/php.ini
sed -i 's/upload_max_filesize = 2M/upload_max_filesize = 100M/g' /etc/php/7.4/apache2/php.ini
````
````bash
sed -i 's|;date.timezone =|date.timezone = America/Chicago|g' /etc/php/7.4/fpm/php.ini
sed -i 's|;date.timezone =|date.timezone = America/Chicago|g' /etc/php/7.4/cli/php.ini
sed -i 's|;date.timezone =|date.timezone = America/Chicago|g' /etc/php/7.4/apache2/php.ini
````
````bash
sed -i 's|;sendmail_path =|sendmail_path = /usr/sbin/sendmail|g' /etc/php/7.4/fpm/php.ini
sed -i 's|;sendmail_path =|sendmail_path = /usr/sbin/sendmail|g' /etc/php/7.4/cli/php.ini
sed -i 's|;sendmail_path =|sendmail_path = /usr/sbin/sendmail|g' /etc/php/7.4/apache2/php.ini
````
````bash
sed -i 's|mysqli.default_socket =|mysqli.default_socket = /var/run/mysqld/mysqld.sock|g' /etc/php/7.4/fpm/php.ini
sed -i 's|mysqli.default_socket =|mysqli.default_socket = /var/run/mysqld/mysqld.sock|g' /etc/php/7.4/cli/php.ini
sed -i 's|mysqli.default_socket =|mysqli.default_socket = /var/run/mysqld/mysqld.sock|g' /etc/php/7.4/apache2/php.ini
````
````bash
sed -i 's/mysqli.default_host =/mysqli.default_host = localhost/g' /etc/php/7.4/fpm/php.ini
sed -i 's/mysqli.default_host =/mysqli.default_host = localhost/g' /etc/php/7.4/cli/php.ini
sed -i 's/mysqli.default_host =/mysqli.default_host = localhost/g' /etc/php/7.4/apache2/php.ini
````
````bash
sed -i 's/mysqli.default_user =/mysqli.default_user = root/g' /etc/php/7.4/fpm/php.ini
sed -i 's/mysqli.default_user =/mysqli.default_user = root/g' /etc/php/7.4/cli/php.ini
sed -i 's/mysqli.default_user =/mysqli.default_user = root/g' /etc/php/7.4/apache2/php.ini
````
````bash
sed -i 's/mysqli.default_pw =/mysqli.default_pw = /g' /etc/php/7.4/fpm/php.ini
sed -i 's/mysqli.default_pw =/mysqli.default_pw = /g' /etc/php/7.4/cli/php.ini
sed -i 's/mysqli.default_pw =/mysqli.default_pw = /g' /etc/php/7.4/apache2/php.ini
````

<br>

# Loop over a Question until the Correct Answer is Received

<br>

````bash
echo "Enter the Path to the directory you want to password protect:"
    read web_dir
    while [ ! -d "$web_dir" ] ; do
        echo "The path you entered, $web_dir, could not be found. Check the spelling and try again."
        sleep 5
        echo "Enter the Path to the Directory you want to password protect:"
        read web_dir
    done
````

# Break down an array to one Element per line

<br>

````bash
printf "%s\n" "${array[@]}"
````