# Axpo Flight Check Platform

This repository orchestrates the full-stack **Axpo Flight Check Platform**, combining:

- A Flask-based backend API serving geospatial asset data from CSV
- A React + Vite frontend for checking drone flight area restrictions and population density

This setup uses **Docker Compose** to simplify local development and deployment. With one command, both services are up and running.


## Tech Stack

**Frontend**
- React 19, TypeScript
- Vite
- Tailwind CSS
- Recharts
- Cypress (testing)

**Backend**
- Python 3.11
- Flask + Gunicorn
- CSV-to-JSON API
- Flask-CORS

**Infrastructure**
- Docker
- Docker Compose
- NGINX (for frontend)


## Quick Start

### 1. Clone this deployment repo

```bash
git clone https://github.com/your-org/axpo-flight-platform.git
cd axpo-flight-platform
```

> This repo includes both frontend and backend as Git submodules.

### 2. Clone submodules (if using Git submodules)

```bash
git submodule update --init --recursive
```

### 3. Start all services

```bash
docker compose up --build
```

### 4. Access the apps

- Frontend: [http://localhost:3000](http://localhost:3000)
- Backend API: [http://localhost:8000/api/assets](http://localhost:8000/api/assets)


## Project Structure

```
axpo-flight-platform/
├── backend/               # Flask REST API (submodule or folder)
│   ├── app.py
│   ├── assets.csv
│   └── Dockerfile
│
├── frontend/              # React frontend app (submodule or folder)
│   ├── src/
│   ├── public/
│   └── Dockerfile
│
├── docker-compose.yml     # Docker orchestration
└── README.md
```


## Environment Variables

The frontend expects a `.env` file inside `frontend/` with the following:

```
VITE_GEOADMIN_BASE=...
VITE_DRONE_LAYER=...
VITE_POP_LAYER=...
VITE_LANG=...
VITE_TOLERANCE=...
VITE_RETURN_GEOMETRY=...
VITE_SRID=...
VITE_LOCATIONS_API_URL=http://localhost:8000/api/assets
```

Adjust `VITE_LOCATIONS_API_URL` as needed to match the Docker service.


## Testing

From inside the `frontend/` directory:

```bash
npm run cypress:open     # Opens the Cypress test runner
npm run cypress:run      # Runs E2E tests in headless mode
```


## Deployment

You can deploy each service independently with Vercel or a VPS, or together using this repo on a container hosting provider.


## API Reference

### `GET /api/assets`

Returns a list of geospatial assets with metadata.

```json
[
  {
    "id": "VL35",
    "name": "Glovelier",
    "type": "run-of-river",
    "latitude": 46.105880590640965,
    "longitude": 7.809260581732722
  }
]
```

## Contributing

Each submodule (frontend/backend) should follow its own contribution and coding guidelines. This repo is for orchestration and deployment only.
