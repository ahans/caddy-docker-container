# Deploy Web Services in Docker Containers Behind a Caddy Frontend

This repository contains an example of how to deploy web services in Docker
containers on a single host and have an instance of
[Caddy](https://caddyserver.com/) in another container as the frontend.


## Provided Services

The example contains two web servers serving static content (one nginx,
the other thttpd, different ones just to show that this is easily possible).
The static content is placed under `www` and made available via `sftp` through
an instance of [sftpgo](https://github.com/drakkan/sftpgo). sftpgo's SSH
port is exposed at 2222, while its web interface is handled by Caddy. There
is also a (Wordpress)[https://hub.docker.com/_/wordpress] container as an
example of something a bit more complicated.


## Setup

To run the example, you need a number of publicly reachable (sub-) domain
names. Edit `config/Caddyfile` and replace the `*.example.com` entries with
yours. Then, start everything up:

```
docker-compose up -d
```

You can now reach the static web containers under the respective
addresses. Caddy will take care of getting
[Letsencrypt](https://letsencrypt.org/) certificates for you.
The `restart: always` entries will make the Docker daemon restart
your containers on system boot.

To stop everything, run:
```
docker-compose down
```
