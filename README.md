# Bitcoin Core Node with Nginx Reverse Proxy

This Docker Compose setup provides a Bitcoin Core node with a secure Nginx reverse proxy that handles SSL termination for JSON-RPC calls.

## Features

- Bitcoin Core node with JSON-RPC enabled
- Nginx reverse proxy with automatic SSL certificate management via certbot
- Secure HTTPS access to Bitcoin Core JSON-RPC API

## Prerequisites

- Docker and Docker Compose
- Domain name pointing to your server
- Basic understanding of Bitcoin Core and nginx configuration

## Setup

1. Clone this repository
2. Copy `.env.example` to `.env` and fill in the required values:
   ```
   RPC_AUTH=your_rpc_auth_string
   RPC_PASSWORD=your_rpc_password
   ```

3. Update the nginx configuration in `user_conf.d/` with your:
   - Domain name
   - Bitcoin Core RPC authentication token

4. Configure `nginx-certbot.env` with your:
   - Email address for Let's Encrypt notifications
   - Domain name

5. Start the services:
   ```bash
   docker compose up -d
   ```

## Security Notice

⚠️ **Work in Progress**: Currently, all Bitcoin Core RPC endpoints are exposed through the proxy. Future updates will include endpoint whitelisting for enhanced security.

## Data Persistence

Bitcoin blockchain data is stored in `/data/btc` on the host machine.
SSL certificates are stored in a Docker volume named `nginx_secrets`.

## Ports

- Bitcoin Core: 8332 (RPC), 8333 (P2P)
- Nginx: 80 (HTTP), 443 (HTTPS)