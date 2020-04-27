# Useful files to keep on your Raspberry Pi

Use these files as examples and modify them to fit your needs.

Place the executable files in `/usr/local/sbin` and save `index.txt` as
`/root/index.html`.

## index.txt

This file contains the website that is shown when you stop the dashboard. It gets
copied into the webroot of your webserver -- make sure your webserver reads
`index.html` files **before** `index.php` files.

## dashboard

Executable file. Make sure to `chmod +x` this file.

Start or stop the dashboard with this command. This toggles the systemd service

- php7.3-fpm.service

Usage:

```
/usr/local/sbin/dashboard {on|off}
```

## hotspot

Executable file. Make sure to `chmod +x` this file.

Start or stop your hotspot. This toggles the systemd services

- mmdvmhost.timer
- mmdvmhost.service

Additionally it starts or stops the dashboard command mentioned above.

Usage:

```
/usr/local/sbin/hotspot {on|off}
```

### Start and stop the hotspot via Cron

Place these lines in your `/etc/crontab` to automatically start and/or stop
your hotspot.

```
30 6  * * 1-5 root  /usr/local/sbin/hotspot off
0 18  * * 1-5 root  /usr/local/sbin/hotspot on
```

That might stop the hotspot at 6:30 and start it again at 18:00, Monday to Friday.

## shrinklog

Executable file. Make sure to `chmod +x` this file.

This command shrinks the MMDVMHost log file to a limited number of important
lines.

The code of this was primarily taken from [Pi-Star][shrinklog] and modified.

[shrinklog]: https://github.com/AndyTaylorTweet/Pi-Star_Binaries_sbin/blob/master/pistar-hourly.cron

Usage:

```
/usr/local/sbin/shrinklog
```