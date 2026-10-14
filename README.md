# gh-docker-demo

A small Node.js + Express application that demonstrates containerized deployment with Docker and GitHub Actions. The app exposes a simple event API and stores data in MongoDB.

## Overview

This project is intended as a demo for:

- building and shipping a Docker image
- running a Node.js service in a container
- integrating Docker-based deployment with GitHub Actions
- connecting a lightweight backend to MongoDB

## Tech Stack

- Node.js 16
- Express
- MongoDB Node.js driver
- Docker
- Playwright (for automated tests)

## Project Structure

```text
.
├── .github/
│   └── workflows/
├── data/
│   └── database.js
├── routes/
│   └── events.js
├── app.js
├── Dockerfile
├── package.json
├── package-lock.json
├── playwright.config.js
├── .gitignore
└── README.md
```

## Features

- `GET /` returns all events from MongoDB
- `POST /` creates a new event record
- Containerized runtime using Docker
- Environment-driven MongoDB configuration

## Prerequisites

Before running this application locally, make sure you have:

- Node.js 16 or later
- npm
- Docker
- A MongoDB instance or MongoDB Atlas cluster

## Local Setup

1. Clone the repository
   ```bash
   git clone https://github.com/damonx/gh-docker-demo.git
   cd gh-docker-demo
   ```

2. Install dependencies
   ```bash
   npm install
   ```

3. Set environment variables
   ```bash
   export PORT=3000
   export MONGODB_CONNECTION_PROTOCOL=mongodb+srv
   export MONGODB_DB_NAME=gha-demo1
   export MONGODB_CLUSTER_ADDRESS=your-cluster.mongodb.net
   export MONGODB_USERNAME=your-username
   export MONGODB_PASSWORD=your-password
   ```

4. Start the app
   ```bash
   npm start
   ```

5. The API will be available at:
   ```bash
   http://localhost:3000
   ```

## API Examples

### Get all events

```bash
curl http://localhost:3000/
```

### Create an event

```bash
curl -X POST http://localhost:3000/ \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Demo Event",
    "type": "test",
    "status": "created"
  }'
```

## Docker

Build the Docker image:

```bash
docker build -t gh-docker-demo .
```

Run the container:

```bash
docker run -p 3000:3000 \
  -e PORT=3000 \
  -e MONGODB_CONNECTION_PROTOCOL=mongodb+srv \
  -e MONGODB_DB_NAME=gha-demo1 \
  -e MONGODB_CLUSTER_ADDRESS=your-cluster.mongodb.net \
  -e MONGODB_USERNAME=your-username \
  -e MONGODB_PASSWORD=your-password \
  gh-docker-demo
```

## Testing

Run the Playwright test suite:

```bash
npm test
```

## Notes

This repository is a lightweight example for demonstrating GitHub Actions automation around Docker builds and deployment flows. It can be adapted for CI/CD pipelines, staging environments, and container-based application delivery.

## License

This project uses the ISC license as defined in `package.json`.
