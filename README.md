# youtrack-docker-compose
Compose to create working [YouTrack](https://www.jetbrains.com/youtrack/) server

![state](https://img.shields.io/badge/state-stable-brightgreen.svg)
![ssl](https://img.shields.io/badge/SSL-OK-brightgreen.svg)
![Version](https://img.shields.io/badge/YouTrack%20ver.%3A-2018.2.45513-brightgreen.svg)

**This configuration use official YouTrack image**

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
mkdir -p -m 750 /opt/youtrack/data /opt/youtrack/logs /opt/youtrack/conf /opt/youtrack/backups
chown -R 13001:13001 /opt/youtrack/data /opt/youtrack/logs /opt/youtrack/conf /opt/youtrack/backups
```

### SSL

HTTPs support is ON, by default. All you need is just set your domain name and email variables in `env.example` 
and rename env.example` to `.env`

Don't push `.env` file in public repositories!

HTTPs support provided by Let's Encrypt certificates 
(see https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion) 
```
VIRTUAL_HOST=youtrack.example.com
LETSENCRYPT_HOST=youtrack.example.com

LETSENCRYPT_EMAIL=username@example.com
```

## Building and setup

Next, build the images:
```
cd youtrack-docker-compose
docker-compose build --pull
```
All working folders will be mapped to `/opt/youtrack/*` on a host.

Now you can Up the service and continue settings in Web Interface:
```
docker-compose up -d
```

**Note: First start can take a long time. Check logs to be sure everything ok:**
```
docker-compose logs -f
```

After initialisation Web Interface will be available on `https://yourdockerhost/`

Note: your SSL certs will be saved in ./nginx/certs folder.

## Contributing

Bug reports, bug fixes and new features are always welcome.
Please open issues and submit pull requests for any new code.
