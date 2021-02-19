# Zabbix MySQL partitioning perl script

Disclaimer: This script isn't made by us, but the current author is unknown. We've added it to Github for ease of access. If you are the original creator of this script, please send us a private message. With that out of the way, let's move on.

This is a script written in Perl to partition the Zabbix database tables. We can use this script to replace the Zabbix housekeeper process with the use of fixed History and Trend storage periods for all items.

## How to use the script
Make sure to partition the database first, if you do not know how. Check out this blog post:
https://blog.zabbix.com/partitioning-a-zabbix-mysql-database/13531/

Place the script in:
```
/usr/share/zabbix/
```

Then make it executable with:
```
chmod +x /usr/share/zabbix/mysql_zbx_part.pl
```

Then add a cronjob with:
```
crontab -e
```

Add the following line:
```
0 23 * * * /usr/share/zabbix/mysql_zbx_part.pl >/dev/null 2>&1
```

We also need to install some Perl dependencies with:

```
yum install perl-DateTime perl-Sys-Syslog

```

or on Debian based systems
```
apt-get install libdatetime-perl liblogger-syslog-perl
```


That's it! You are now done and you have setup MySQL partitioing. We could execute the script manually with:
```
perl /usr/share/zabbix/mysql_zbx_part.pl
```

Then we can check and see if it worked with:
```
journalctl -t mysql_zbx_part
```
