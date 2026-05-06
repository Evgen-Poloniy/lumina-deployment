# LLM Service Deployment (lumina-deployment)

This repository contains Docker-based deployment configuration for the **Lumina LLM platform**, including:

- Keycloak (authentication)
- PostgreSQL (database for IdP)
- Redis (cache)
- LLM REST API service
- API Gateway

---

## Requirements

- Docker
- Docker Compose
- Make (optional but recommended)

---

## Quick Start

Start the full stack:

```bash
make up
```

or

```bash
docker compose up --build
```

Stop the stack:

```bash
make down
```

or

```bash
docker compose down
```

> Note: Ensure your Makefile includes a proper `down` target.

---

## Environment Variables

You must define the following environment variables before running the system.

---

### Keycloak

```env
KC_HOSTNAME=http://localhost:4000   # Public Keycloak URL used by clients
KC_BOOTSTRAP_ADMIN_USERNAME=        # Initial admin username
KC_BOOTSTRAP_ADMIN_PASSWORD=        # Initial admin password
KC_HOST=0.0.0.0                     # Keycloak bind address inside container
KC_PORT=4000                        # Keycloak exposed port
```

---

### PostgreSQL

```env
DB_PASSWORD=   # Password for PostgreSQL database user
```

---

### LLM API Service

```env
LLM_DIR_PATH=../lumina-REST-API   # Path to LLM REST API source code

LLM_API_KEY=                      # API key for LLM service authentication

LLM_API_HOST=0.0.0.0             # Bind address for LLM API service
LLM_API_PORT=5600                # Port exposed by LLM API service
```

---

### API Gateway

```env
GATEWAY_DIR_PATH=../lumina-platform  # Path to API gateway source code

LLM_URL=http://lumina-rest-api:5600  # Internal URL of LLM service (Docker network)

GATEWAY_API_HOST=0.0.0.0             # Bind address for gateway service
GATEWAY_API_PORT=8080                # Gateway exposed port

CLIENT_SECRET=                       # Secret used for client authentication (OAuth / Keycloak integration)
```

---

### Redis Cache

```env
REDIS_HOST=0.0.0.0     # Redis host address (container network)
REDIS_PORT=6379        # Redis port
REDIS_PASSWORD=        # Redis password (optional if not enabled)
```

---

## Services Overview

| Service       | Description |
|--------------|-------------|
| Keycloak     | Authentication and identity management |
| Postgres     | Persistent storage for keycloak data |
| Redis        | Caching layer for fast access |
| LLM API      | Core LLM inference REST service |
| API Gateway  | Entry point for clients, routes requests to services |

---
