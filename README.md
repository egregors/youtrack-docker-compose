# youtrack-docker-compose
Compose to create working [YouTrack](https://www.jetbrains.com/youtrack/) server

![state](https://img.shields.io/badge/state-stable-brightgreen.svg)
![ssl](https://img.shields.io/badge/HTTPs-traefik-brightgreen.svg)
![Version](https://img.shields.io/badge/YouTrack%20ver.%3A-2020.2.7479-brightgreen.svg)

**This configuration use official images**

[YouTrack](https://hub.docker.com/r/jetbrains/youtrack)
[Traefik](https://hub.docker.com/_/traefik)

# How to use

Clone this repository or download the zip.

```
git clone https://github.com/Egregors/youtrack-docker-compose.git
```

## Configuration

### Create and Configure YouTrack-specific Directories

They must be accessible to the user account that is used to run YouTrack service inside the container. 
YouTrack uses the non-root account 13001:13001 (group:id, respectively).
```
mkdir -p /srv/letsencrypt && mkdir -p -m 750 /srv/youtrack/{data,conf,backups,logs} && chown -R 13001:13001 /srv/youtrack
```

### SSL

HTTPs entry point is enabled by default thanks to [traefik](https://traefik.io/). 
All you need is just set your domain name and email variables in `env.example` 
and rename env.example to `.env`

Don't push `.env` file in public repositories!

```
VIRTUAL_HOST=youtrack.example.com

LETSENCRYPT_HOST=youtrack.example.com
LETSENCRYPT_EMAIL=username@example.com
```

## Building and setup

Next, build the images: `make build`

or

```
docker-compose build --pull
```

All working folders will be mapped to `/opt/youtrack/*` on a host.

Now you can Up the service and continue settings in Web Interface: `make up`

or 

```
docker-compose up -d && docker-compose logs -f -t --tail=10
```

**Note: First start can take a long time. Check logs to be sure everything ok:**

After initialisation Web Interface will be available on `https://yourdockerhost/`

Note: your SSL certs will be saved in /srv/letsencrypt folder.

## Contributing

Bug reports, bug fixes and new features are always welcome.
Please open issues and submit pull requests for any new code.
