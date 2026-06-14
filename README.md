# 🐳 MoviCol Infra

Orquestación Docker Compose para todo el stack MoviCol.

## Servicios

| Servicio | Puerto | Descripción |
|----------|--------|-------------|
| PostGIS | 5432 | Base de datos espacial |
| AI | 8000 | GNN predictions + agente LLM (FastAPI) |
| Backend | 3001 | API Gateway + WebSocket (NestJS) |
| Frontend | 3000 | UI React + Leaflet (Nginx) |

## Quick Start

```bash
# 1. Configurar
cp .env.example .env
# Editar .env → agregar OPENAI_API_KEY (opcional)

# 2. Levantar (build desde source)
docker compose -f docker-compose.dev.yml up -d --build

# 3. Verificar
docker compose -f docker-compose.dev.yml ps
curl http://localhost:8000/health    # AI
curl http://localhost:3001/health    # Backend
open http://localhost:3000           # Frontend
```

## URLs

| Servicio | URL |
|----------|-----|
| Frontend | http://localhost:3000 |
| Backend API | http://localhost:3001 |
| Swagger Backend | http://localhost:3001/api/docs |
| AI API | http://localhost:8000 |
| Swagger AI | http://localhost:8000/docs |

## Comandos

```bash
docker compose -f docker-compose.dev.yml up -d --build   # Levantar
docker compose -f docker-compose.dev.yml down            # Parar
docker compose -f docker-compose.dev.yml logs -f ai      # Logs AI
docker compose -f docker-compose.dev.yml ps              # Estado
```

## Sin Docker (desarrollo local)

```bash
# Terminal 1: AI
cd ../movicol-ai && make dev

# Terminal 2: Backend
cd ../movicol-backend && npm run dev

# Terminal 3: Frontend
cd ../movicol-frontend && npm run dev
```

## Pipeline ML

```bash
cd ../movicol-ai
make clean-graph   # Limpiar grafo
make train         # Entrenar modelo GAT
make test          # Verificar
```
