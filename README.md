# mastodon-traefikv2-docker-compose
Mastodon Instance based on Docker Compose. Requires a Traefik Load Balancer

## Demo

Visit https://r-kara.de for a demo of my own Mastodon Instance

## Install

Configure the Docker-Compose File:

Variables to fill in:

- External network mapping "Proxy": Change the external network mapping to the Network that your traefik instance is in.
- <POSTGRES_PASSWORD> - the password for the postgres db. Use the same during mastodon:setup!
- <DOMAIN> - e.g. social.yourdomain.com (Must have an A record pointing to your box' IP) (AAAA for IPv6 ;)
- (Optional) Volume Mapping - You can change Volumes of every Container but changing the first path e.g. ./mastodon-data/postgres to /opt/anyfolder/postgres
- Traefik Configuration - You may have to change the Traefik Labels according to your configuration. If you have a catch all rule for http for example,  you may remove the redirection rule


Download my docker-compose.yml and fill in the variables to your needs

In the same directory run:

```touch .env.production```

Alternatively, you can copy the .env.production.sample from this repo, fill it up to your likings and afterwards rename it to ```.env.production```

On linux machines: ```sudo chown 991:991 .env.production```

```docker-compose run --rm -v $(pwd)/.env.production:/opt/mastodon/.env.production web bundle exec rake mastodon:setup```

This will guide you through some steps setting up things like Users, Secrets, etc. don’t worry.

```docker-compose up -d```

That should be it. You now have an instance of Mastodon running behind a traefik reverse-proxy handling HTTPS redirection, TLS termination and automagic setup and renewal of Let’s Encrypt certificates. Persistence data from the containers is stored in folders located in the same directory as your docker-compose.yml.
