# Pi-Hole + Unbound - 1 Container

## Description

This Docker deployment runs both Pi-Hole and Unbound in a single container.

The base image for the container is the [official Pi-Hole container](https://hub.docker.com/r/pihole/pihole), with an extra build step added to install the Unbound resolver directly into to the container based on [instructions provided directly by the Pi-Hole team](https://docs.pi-hole.net/guides/unbound/).

## Usage

First create a `.env` file to substitute variables for your deployment.

### Pi-hole environment variables

> Vars and descriptions replicated from the [official pihole container](https://github.com/pi-hole/docker-pi-hole/#environment-variables):

| Variable | Default | Value | Description |
| -------- | ------- | ----- | ---------- |
| `TZ` | UTC | `<Timezone>` | Set your [timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) to make sure logs rotate at local midnight instead of at UTC midnight.
| `WEBPASSWORD` | random | `<Admin password>` | <http://pi.hole/admin> password. Run `docker logs pihole \| grep random` to find your random pass.
| `FTLCONF_LOCAL_IPV4` | unset | `<Host's IP>` | Set to your server's LAN IP, used by web block modes and lighttpd bind address.
| `REV_SERVER` | `false` | `<"true"\|"false">` | Enable DNS conditional forwarding for device name resolution |
| `REV_SERVER_DOMAIN` | unset | Network Domain | If conditional forwarding is enabled, set the domain of the local network router |
| `REV_SERVER_TARGET` | unset | Router's IP | If conditional forwarding is enabled, set the IP of the local network router |
| `REV_SERVER_CIDR` | unset | Reverse DNS | If conditional forwarding is enabled, set the reverse DNS zone (e.g. `192.168.0.0/24`) |
| `WEBTHEME` | `default-light` | `<"default-dark"\|"default-darker"\|"default-light"\|"default-auto"\|"lcars">`| User interface theme to use.

Example `.env` file in the same directory as your `docker-compose.yaml` file:

```yaml
FTLCONF_LOCAL_IPV4=10.69.42.4
TZ=Europe/Brussels
WEBPASSWORD=pihole
REV_SERVER=true
REV_SERVER_DOMAIN=home.local
REV_SERVER_TARGET=10.69.42.1
REV_SERVER_CIDR=10.69.42.0/24
HOSTNAME=pihole
DOMAIN_NAME=home.local
PIHOLE_WEBPORT=8000
WEBTHEME=default-dark
```
