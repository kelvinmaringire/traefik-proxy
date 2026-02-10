# Traefik (central proxy) – one token for all domains

Use a **single** Cloudflare API token in `.env` as `CF_DNS_API_TOKEN`. The container receives it as `CLOUDFLARE_DNS_API_TOKEN` for ACME.

- Create one token in Cloudflare with **Zone: Zone / Read** and **Zone: DNS / Edit**, scoped to **All zones** (or include every zone you use).
- That one token is used for every domain (ruzivoflow.com, etc.); Traefik does not support different tokens per domain in one instance.
- If domains live in different Cloudflare accounts, use one token that has access to all zones, or run a separate Traefik per account.

```bash
docker network create traefik_net

chmod 600 ./data/certs/cloudflare-acme.json
chown root:root ./data/certs/cloudflare-acme.json


```


## Clone and Setup Treafik Project

```bash
mkdir -p ~/srv

cd ~/srv

sudo git clone https://github.com/kelvinmaringire/traefik-proxy.git

cd traefik-proxy

nano .env   # (paste your environment variables here)

docker compose up -d
```
