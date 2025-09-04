🚀 Inventory Management System

This project contains a **Spring Boot backend** (Java 17), **Angular frontend**, and uses **Postgres** + **Redis** as dependencies.
It is fully containerized with **Docker Compose**.


## 📦 Prerequisites

Make sure you have the following installed:

* [Docker](https://docs.docker.com/get-docker/)
* [Docker Compose](https://docs.docker.com/compose/install/)
* [Git](https://git-scm.com/downloads)

## 🔹 Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/<your-org>/<your-repo>.git
cd <your-repo>
```

### 2. Run with Docker Compose

#### 🛠️ Development (build images locally)

```bash
docker compose -f docker-compose.yml up --build -d
```

This will:

* Build the **backend** from source (Maven + Spring Boot)
* Build the **frontend** (Angular + Nginx)
* Start **Postgres** and **Redis**


#### 🚀 Production (use prebuilt images from Docker Hub)

```bash
docker compose -f docker-compose.prod.yml up -d
```

This will pull prebuilt images from Docker Hub and start everything quickly.


### 3. Verify containers are running

```bash
docker ps
```

Expected services:

* **frontend** → port `80`
* **backend** → port `8080`
* **postgres** → port `5432` (internal)
* **redis** → port `6379` (internal)


### 4. Access the application

* Frontend (UI): 👉 [http://localhost](http://localhost)
* Backend API: 👉 [http://localhost:8080](http://localhost:8080)


## 🐳 Docker Hub Workflow

### Push images (done by maintainer)

```bash
# Login to Docker Hub
docker login

# Tag images (example for backend & frontend)
docker tag backend-backend:latest vipink18/backend:latest
docker tag backend-frontend:latest vipink18/frontend:latest

# Push to Docker Hub
docker push vipink18/backend:latest
docker push vipink18/frontend:latest
```


### Pull images (done by teammates)

Your teammates don’t need to build locally. They just run:

```bash
docker compose -f docker-compose.prod.yml up -d
```

Docker Compose will:

* Pull `vipink18/backend:latest`
* Pull `vipink18/frontend:latest`
* Start Postgres & Redis automatically


## 🔄 Useful Commands

* Stop all containers (but keep volumes):

  ```bash
  docker compose down
  ```

* Stop and remove containers + volumes:

  ```bash
  docker compose down -v
  ```

* View logs:

  ```bash
  docker compose logs -f
  ```

* Rebuild everything from scratch:

  ```bash
  docker system prune -af --volumes
  ```

* If `6379` (Redis) or `5432` (Postgres) are **already in use** on your system, update `docker-compose.yml` to use different host ports (or remove port mapping if not needed).
* For production, only **frontend (80)** and **backend (8080)** are exposed; Postgres and Redis stay internal.