# Deploy WorkAdventure em VPS

Este diretório contém a stack Docker para rodar o WorkAdventure em uma VPS com Docker instalado.

## Passo a passo

1. Copie o arquivo de variáveis de exemplo:
   ```bash
   cd deploy/vps
   cp .env.example .env
   ```
2. Edite `.env` preenchendo `DOMAIN`, chaves secretas e credenciais do servidor TURN.
3. Crie os diretórios de dados persistentes (armazenados fora dos contêineres):
   ```bash
   mkdir -p ../../docker-data/map-storage ../../docker-data/nginx/logs
   ```
4. Suba os serviços:
   ```bash
   docker compose up -d
   ```

## Portas que precisam ser liberadas

- TCP 80 (HTTP)
- TCP 443 (HTTPS)
- UDP 3478 (coturn)

Caso utilize firewall (ufw/iptables), certifique-se de liberar as portas acima.

## Instalação rápida do Docker no Ubuntu

```bash
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker "$USER"
newgrp docker
```

Depois da instalação, confirme se o plugin do Docker Compose V2 está disponível (`docker compose version`).

- Abrir portas no VPS: TCP 80, TCP 443, UDP 3478 e TCP 3478.
- Criar diretórios persistentes antes do compose:
  mkdir -p ../../docker-data/map-storage ../../docker-data/nginx/logs
- Copiar env:
  cd deploy/vps && cp .env.example .env && editar valores.
- Subir stack:
  docker compose up -d
- Depois configurar SSL (vamos adicionar Nginx + Certbot em etapa seguinte).
