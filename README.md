# youtrack-docker-compose
Compose to create working [YouTrack](https://www.jetbrains.com/youtrack/) server

**YouTrack Dockerfile for this compose based on [this](https://github.com/uniplug/youtrack-docker) repo**

Current YouTrack version: **2017.4.37933**

# How to use

Clone this repository or download the zip.

```
git clone https://github.com/Egregors/youtrack-docker-compose.git
```

## Configuration

All you need is just setup your domain and email for HTTPs(SSL) support.

HTTPs support provided by Let's Encrypt certificates 
(see https://github.com/JrCs/docker-letsencrypt-nginx-proxy-companion) 
just set your domain name and email for `nginx` service in compose file:

```
  nginx:
    image: nginx
    links:
        - youtrack
    ports:
        - "80:80"
        - "443:443"
    volumes:
        - "./nginx/html:/usr/share/nginx/html"
        - "./nginx/certs:/etc/nginx/certs"
        - "./nginx/vhost.d:/etc/nginx/vhost.d"
        - "./nginx/conf.d:/etc/nginx/conf.d"
    environment:
         # set your domain name and email!
         VIRTUAL_HOST: localhost
         LETSENCRYPT_HOST: localhost
         LETSENCRYPT_EMAIL: example@domain.com
```

## Building and setup

Next, build the images:

```
cd youtrack-docker-compose
docker-compose build --push
```

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

Bug reports, bug fixes, and new features are always welcome.
Please 