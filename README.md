# 🐳 MoviCol Infra

Orquestación Docker Compose para todo el stack MoviCol.

## Servicios

| Servicio | Imagen | Puerto | Descripción |
|----------|--------|--------|-------------|
| PostGIS | `postgis/postgis:16-3.4` | 5432 | Base de datos espacial |
| AI | `colombolabs/movicol-ai:latest` | 8000 | GNN + agente LLM |
| Backend | `colombolabs/movicol-backend:latest` | 3001 | API Gateway + WebSocket |
| Frontend | `colombolabs/movicol-frontend:latest` | 3000 | UI React |

## Quick Start

```bash
cp .env.example .env
# Editar .env → agregar OPENAI_API_KEY

docker compose up -d

# Verificar
docker compose ps
```

## URLs

| Servicio | URL |
|----------|-----|
| Frontend | http://localhost:3000 |
| Backend API | http://localhost:3001 |
| Swagger Backend | http://localhost:3001/api/docs |
| AI API | http://localhost:8000 |
| Swagger AI | http://localhost:8000/docs |

## Variables de entorno

```env
POSTGRES_USER=movicol
POSTGRES_PASSWORD=movicol_dev
POSTGRES_DB=movicol
OPENAI_API_KEY=sk-xxx
```

## Comandos útiles

```bash
docker compose up -d          # Levantar todo
docker compose down           # Parar todo
docker compose logs -f ai     # Ver logs del AI service
docker compose ps             # Estado de servicios
```

## Requisitos

- Docker 24+
- Docker Compose v2
