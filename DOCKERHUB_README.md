# CloudFlow Frontend

[![Docker Pulls](https://img.shields.io/docker/pulls/ahmedmusa/cloudflow-frontapp)](https://hub.docker.com/r/ahmedmusa/cloudflow-frontapp)
[![Docker Image Size](https://img.shields.io/docker/image-size/ahmedmusa/cloudflow-frontapp/latest)](https://hub.docker.com/r/ahmedmusa/cloudflow-frontapp)

A modern, responsive Next.js 16 frontend for user profile management with a beautiful UI built with React 19 and Tailwind CSS.

## Quick Start

```bash
docker pull ahmedmusa/cloudflow-frontapp:latest
docker run -p 3000:3000 \
  -e NEXT_PUBLIC_API_URL="http://localhost:3001" \
  -e NODE_ENV="development" \
  ahmedmusa/cloudflow-frontapp:latest
```

## Features

- **Next.js 16** - Latest React framework with App Router
- **React 19** - Modern React with improved performance
- **TypeScript** - Full type safety
- **Tailwind CSS 4** - Utility-first styling
- **shadcn/ui** - Beautiful pre-built components
- **Responsive Design** - Mobile-first approach
- **Lightweight** - Based on Node.js Alpine

## Environment Variables

| Variable              | Required | Description      | Example                 |
| --------------------- | -------- | ---------------- | ----------------------- |
| `NEXT_PUBLIC_API_URL` | Yes      | Backend API URL  | `http://localhost:3001` |
| `NODE_ENV`            | No       | Environment mode | `development`           |
| `PORT`                | No       | Server port      | `3000`                  |

## Docker Compose Example

```yaml
services:
  mongodb:
    image: mongo:7
    container_name: cloudflow-mongodb
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password
      MONGO_INITDB_DATABASE: cloudflow
    volumes:
      - mongo_data:/data/db
    networks:
      - cloudflow-network

  api:
    image: ahmedmusa/cloudflow-api:latest
    container_name: cloudflow-api
    ports:
      - "3001:3001"
    environment:
      MONGO_URI: mongodb://admin:password@mongodb:27017/cloudflow?authSource=admin
      DB_NAME: cloudflow
      FRONTEND_ORIGINS: http://localhost:3000
    depends_on:
      - mongodb
    networks:
      - cloudflow-network

  frontend:
    image: ahmedmusa/cloudflow-frontapp:latest
    container_name: cloudflow-frontapp
    ports:
      - "3000:3000"
    environment:
      NEXT_PUBLIC_API_URL: http://localhost:3001
    depends_on:
      - api
    networks:
      - cloudflow-network

volumes:
  mongo_data:

networks:
  cloudflow-network:
    driver: bridge
```

## Running with Environment File

Create a `.env` file:

```
NEXT_PUBLIC_API_URL=http://localhost:3001
NODE_ENV=development
PORT=3000
```

Run with:

```bash
docker run --env-file .env -p 3000:3000 ahmedmusa/cloudflow-frontapp:latest
```

## Access

Once running, open your browser and navigate to:

```bash
http://localhost:3000
```

## Source Code

- GitHub: https://github.com/iAhmedMusa/clowflow-frontend

## Supported Tags

- `latest` - Latest stable release
- `v1.0.0` - Version tags (coming soon)

## License

MIT License - See GitHub repository for details.
