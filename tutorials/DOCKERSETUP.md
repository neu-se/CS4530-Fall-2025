---
layout: page
title: Docker Setup Guide
permalink: /tutorials/docker-setup
parent: Tutorials
nav_order: 7
---

# Tutorial: Docker Setup Guide

## Contents
- [Introduction](#introduction)
- [Architecture Overview](#architecture-overview)
- [Docker Compose Configuration](#docker-compose-configuration)
- [Server Dockerfile](#server-dockerfile)
- [Client Dockerfile](#client-dockerfile)
- [Usage Instructions](#usage-instructions)
- [Development Workflow](#development-workflow)
- [Troubleshooting](#troubleshooting)
- [Production Considerations](#production-considerations)
- [Additional Resources](#additional-resources)

## Introduction

This document explains the Docker configuration for the Fake Stack Overflow application, which consists of three containerized services: MongoDB database, Node.js server, and React client.

## Architecture Overview

The application uses Docker Compose to orchestrate three services:

- **MongoDB**: Database service running MongoDB 7
- **Server**: Node.js/Express backend API (port 8000)
- **Client**: React frontend with Vite dev server (port 5173)

All services are connected through a Docker network and can communicate with each other using service names as hostnames.

## Docker Compose Configuration

The `docker-compose.yml` file at the project root orchestrates all services:

```yaml
version: "3.8"

services:
  mongodb:
    image: mongo:7-jammy
    container_name: fake-stack-overflow-db
    restart: unless-stopped
    ports:
      - "27017:27017"
    volumes:
      - mongodb_data:/data/db
    environment:
      - MONGO_INITDB_DATABASE=fake_so

  server:
    build:
      context: .
      dockerfile: ./server/Dockerfile
    container_name: fake-stack-overflow-server
    restart: unless-stopped
    ports:
      - "8000:8000"
    depends_on:
      - mongodb
    environment:
      - NODE_ENV=development
      - MONGODB_URI=mongodb://mongodb:27017
      - CLIENT_URL=http://localhost:5173
      - PORT=8000
    volumes:
      - ./server:/app/server
      - ./shared:/app/shared
      - /app/server/node_modules

  client:
    build:
      context: .
      dockerfile: ./client/Dockerfile
    container_name: fake-stack-overflow-client
    restart: unless-stopped
    ports:
      - "5173:5173"
    depends_on:
      - server
    environment:
      - NODE_ENV=development
    volumes:
      - ./client:/app/client
      - ./shared:/app/shared
      - /app/client/node_modules

volumes:
  mongodb_data:
```

### Key Configuration Details

- **MongoDB Service**: Uses the official MongoDB 7 image with persistent data storage via named volume
- **depends_on**: Ensures services start in the correct order (MongoDB → Server → Client)
- **volumes**: Bind mounts enable hot-reloading during development
- **node_modules volumes**: Anonymous volumes prevent host node_modules from overriding container's

## Server Dockerfile

Location: `server/Dockerfile`

```dockerfile
FROM node:18-alpine

WORKDIR /app

# Copy root package.json for workspace setup
COPY package*.json ./

# Copy shared package
COPY shared/ ./shared/

# Copy server package files
COPY server/package*.json ./server/

# Install dependencies from root
RUN npm install

# Build shared package
RUN npm run build --workspace=shared

# Copy server source code
COPY server/ ./server/

# Set working directory to server
WORKDIR /app/server

# Expose the port
EXPOSE 8000

# Start development server
CMD ["npm", "run", "dev"]
```

### Server Dockerfile Explanation

1. **Base Image**: Uses `node:18-alpine` for a lightweight container
2. **Workspace Setup**: Copies root package.json to set up npm workspaces
3. **Shared Package**: Copies and builds the shared package used by both client and server
4. **Dependency Installation**: Installs all dependencies from the root workspace
5. **Source Code**: Copies server source code after dependencies for better layer caching
6. **Port**: Exposes port 8000 for the API
7. **Start Command**: Runs the development server with hot-reloading

## Client Dockerfile

Location: `client/Dockerfile`

```dockerfile
FROM node:18-alpine

WORKDIR /app

# Copy root package.json for workspace setup
COPY package*.json ./

# Copy shared package
COPY shared/ ./shared/

# Copy client package files
COPY client/package*.json ./client/

# Install dependencies from root
RUN npm install

# Build shared package
RUN npm run build --workspace=shared

# Copy client source code
COPY client/ ./client/

# Set working directory to client
WORKDIR /app/client

# Expose port 5173 (Vite dev server default)
EXPOSE 5173

# Start development server
CMD ["npm", "run", "dev", "--", "--host", "0.0.0.0"]
```

### Client Dockerfile Explanation

1. **Base Image**: Uses `node:18-alpine` matching the server
2. **Workspace Setup**: Identical workspace configuration as the server
3. **Shared Package**: Builds shared package for type definitions and utilities
4. **Dependency Installation**: Installs all workspace dependencies
5. **Source Code**: Copies client source after dependencies
6. **Port**: Exposes port 5173 for Vite dev server
7. **Start Command**: Runs Vite with `--host 0.0.0.0` to accept external connections

## Usage Instructions

### Starting the Application

To start all services:

```bash
docker-compose up
```

To start in detached mode (background):

```bash
docker-compose up -d
```

To rebuild images before starting:

```bash
docker-compose up --build
```

### Stopping the Application

To stop all services:

```bash
docker-compose down
```

To stop and remove volumes (clears database):

```bash
docker-compose down -v
```

### Viewing Logs

View logs from all services:

```bash
docker-compose logs
```

View logs from a specific service:

```bash
docker-compose logs server
docker-compose logs client
docker-compose logs mongodb
```

Follow logs in real-time:

```bash
docker-compose logs -f
```

### Accessing Services

Once running, you can access:

- **Client**: http://localhost:5173
- **Server API**: http://localhost:8000
- **MongoDB**: localhost:27017

### Rebuilding Containers

If you make changes to package.json or Dockerfiles:

```bash
docker-compose build
docker-compose up
```

Or combine into one command:

```bash
docker-compose up --build
```

### Executing Commands in Containers

Run a command in a running container:

```bash
docker-compose exec server npm run test
docker-compose exec client npm run lint
```

Open a shell in a container:

```bash
docker-compose exec server sh
docker-compose exec client sh
```

## Development Workflow

The Docker setup is optimized for development with the following features:

1. **Hot Reloading**: Both client and server support hot-reloading thanks to bind mounts
2. **Shared Package**: The shared workspace is automatically built and available to both services
3. **Persistent Database**: MongoDB data persists across container restarts
4. **Isolated Dependencies**: Each service has its own node_modules in the container

### Making Code Changes

Simply edit files in your local `client/`, `server/`, or `shared/` directories. Changes will be automatically reflected:

- Client changes trigger Vite HMR (Hot Module Replacement)
- Server changes restart the Node.js process (via nodemon or similar)
- Shared package changes require rebuilding: `npm run build --workspace=shared`

## Troubleshooting

### Port Already in Use

If you see port conflict errors:

```bash
# Find and stop processes using the ports
lsof -ti:5173 | xargs kill  # Client port
lsof -ti:8000 | xargs kill  # Server port
lsof -ti:27017 | xargs kill # MongoDB port
```

### Container Won't Start

Check logs for the failing service:

```bash
docker-compose logs [service-name]
```

### Database Connection Issues

Ensure MongoDB is running and healthy:

```bash
docker-compose ps
```

The server connects to MongoDB using `mongodb://mongodb:27017` (service name as hostname).

### Clean Restart

For a completely fresh start:

```bash
# Stop containers and remove volumes
docker-compose down -v

# Remove images
docker-compose rm -f

# Rebuild and start
docker-compose up --build
```

### Permission Issues

If you encounter permission issues with node_modules:

```bash
# Remove local node_modules
rm -rf client/node_modules server/node_modules shared/node_modules

# Rebuild containers
docker-compose up --build
```

## Production Considerations

This Docker setup is configured for **development** only. For production deployment:

1. Use multi-stage builds to create optimized production images
2. Build client assets statically instead of running dev server
3. Use environment-specific configuration files
4. Add security measures (non-root users, security scanning)
5. Use production-grade process manager (PM2, etc.)
6. Configure proper MongoDB authentication
7. Use secrets management for sensitive data
8. Add health checks to docker-compose.yml

## Additional Resources

- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)
- [Node.js Docker Best Practices](https://github.com/nodejs/docker-node/blob/main/docs/BestPractices.md)
