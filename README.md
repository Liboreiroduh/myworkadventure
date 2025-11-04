# WorkAdventure deployment for Hostinger

This repository packages WorkAdventure with Traefik and a static maps service ready to deploy on a VPS (tested path for Hostinger).

## Repository layout

- `maps/`: base example map (`office.json`) with tileset and assets.
- `deploy/vps/`: production stack (docker compose, Traefik config, maps copy).
- `.env` and `deploy/vps/.env`: environment values already filled for `wa.intienergiaacademy.com.br`.

## Requirements

1. VPS with Docker and Docker Compose.
2. DNS records pointing to the VPS:
   - `wa.intienergiaacademy.com.br`
   - `admin.wa.intienergiaacademy.com.br`
3. Outbound access on ports 80/443 for Let's Encrypt.

## Quick start

```bash
git clone https://github.com/liboreiroduh/myworkadventure.git
cd myworkadventure/deploy/vps
chmod 600 traefik/acme.json
docker compose up -d
```

Services will be reachable at:

- WorkAdventure frontend: `https://wa.intienergiaacademy.com.br/`
- Admin panel: `https://admin.wa.intienergiaacademy.com.br/`
- Maps (static files): `https://wa.intienergiaacademy.com.br/maps/office.json`

## Map customization

Edit the JSON map or tiles inside `maps/` (and sync the copy in `deploy/vps/maps/` if you change assets). Export new Tiled maps to the same structure to expose them automatically via `/maps`.
