# About

You can easily spin up a web server (Caddy server) with a static site service the `csv` files generated by the `BS440csv` plugin. The static site here will render nice graphs using [d3](d3js.org) for the past 30 days.

You can then access the site by surfing to your device: http://your-device-ip:5440/?p=1
(You select the person with the `p` parameter)

# Installation

## Install Caddy server

Url: <https://caddyserver.com/>

Download the correct version of the Caddy server for your platform. After unpacking the archive, copy `caddy` to `/usr/local/bin/caddy` and copy the relevant init file for your platform (eg. `init/linux-systemd/caddy.service` for SystemD based systems)

## Copy the Caddyfile

Copy the `Caddyfile` from this directory to `/etc/caddy/Caddyfile`.

If you would change the static site content's location, you need to update the `Caddyfile`. You may also want to change the http port here (now set to `5440`)

If you would change the location of the `BS440` files, you need to update the `Caddyfile` (so that it can find the `csv` files).

## Copy the static content

Create a directory `/opt/site` and copy `index.html` from here to that directory. You may choose to change `/opt/site` to a different location, but then you need to update `/etc/caddy/Caddyfile`.

## (Re)start the Caddy server

Test manually:

```
/usr/local/bin/caddy -log stdout -agree=true -conf=/etc/caddy/Caddyfile -root=/var/tmp
```

If it doesn't complain, start/enable the service with your servicem management tools.

Eg. for systemd:

```bash
systemctl enable caddy
systemctl start caddy
```