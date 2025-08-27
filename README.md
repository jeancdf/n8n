# n8n on Raspberry Pi with Caddy HTTPS

This repository contains Docker Compose configuration to run n8n on a Raspberry Pi with:

- PostgreSQL database for data persistence
- Caddy reverse proxy for automatic HTTPS with Let's Encrypt
- ARM64 compatible Docker images

## Prerequisites

- Raspberry Pi 4 (or newer) running 64-bit OS
- Docker and Docker Compose installed
- A domain name pointing to your Raspberry Pi's IP address
- Port 80 and 443 forwarded from your router to the Raspberry Pi

## Setup Instructions

1. Clone this repository to your Raspberry Pi:
   ```
   git clone https://github.com/yourusername/n8n.git
   cd n8n
   ```

2. Copy the environment template and edit it:
   ```
   cp env.template .env
   nano .env
   ```

3. Update the `.env` file with your configuration:
   - Set `N8N_DOMAIN` to your actual domain name
   - Set strong passwords and encryption key
   - Add your email address for Let's Encrypt notifications

4. Start the stack:
   ```
   docker-compose up -d
   ```

5. Access n8n at `https://your-domain.com`

## Environment Variables

- `POSTGRES_USER`: PostgreSQL username
- `POSTGRES_PASSWORD`: PostgreSQL password
- `POSTGRES_DB`: PostgreSQL database name
- `N8N_ENCRYPTION_KEY`: Secret key for n8n data encryption (32+ characters)
- `N8N_DOMAIN`: Your domain name (e.g., n8n.example.com)
- `N8N_HOST`: Same as N8N_DOMAIN
- `N8N_PROTOCOL`: https
- `WEBHOOK_URL`: Full URL for webhooks (https://your-domain.com/)
- `CADDY_EMAIL`: Email for Let's Encrypt notifications
- `TZ`: Your timezone

## Updating

To update the stack to the latest versions:

```
docker-compose pull
docker-compose up -d
```

## Persistence

Data is stored in Docker volumes:
- `n8n_data`: n8n workflows and data
- `postgres_data`: PostgreSQL database
- `caddy_data`: SSL certificates and Caddy data
- `caddy_config`: Caddy configuration

## Troubleshooting

- Check logs with: `docker-compose logs -f`
- Specific service logs: `docker-compose logs -f n8n`
- Caddy logs are in the container at `/data/access.log`