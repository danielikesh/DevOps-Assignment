# 01 — Backend Setup & Containerization

## Project Overview

The backend is a simple FastAPI service exposing two endpoints:

* `GET /api/health` — service health status
* `GET /api/message` — integration confirmation message

FastAPI was chosen because it is lightweight, asynchronous by default, and commonly used for microservices and API-based architectures. This makes it suitable for containerized and scalable deployments.

---

## Local Verification (Pre‑Container Check)

Before containerizing, the application was verified locally to ensure the codebase works independently of Docker.

Purpose:

* Confirm application logic works
* Avoid debugging code and infrastructure simultaneously

---

## Dockerization

The application was containerized to ensure environment consistency across local development, CI/CD pipelines, and cloud infrastructure.

### Why Docker

* Eliminates "works on my machine" issues
* Provides reproducible runtime environment
* Required for automated deployments and scaling
* Enables platform‑independent execution

### Dockerfile Explanation

* **Base image (`python:3.11-slim`)**: minimal Python runtime to reduce image size
* **Working directory (`/app`)**: standardized container file structure
* **Copy requirements first**: enables Docker layer caching and faster rebuilds
* **Install dependencies**: ensures deterministic runtime environment
* **Copy source code**: adds application after dependencies to preserve cache
* **Expose port 8000**: FastAPI default service port
* **Uvicorn start command**: production‑style ASGI server startup

---

## Build & Run

Build image:

```
docker build -t fastapi-backend .
```

Run container:

```
docker run -d -p 8000:8000 --name backend fastapi-backend
```

Verification:

* [http://localhost:8000/api/health](http://localhost:8000/api/health)
* [http://localhost:8000/docs](http://localhost:8000/docs)

Expected health response:

```
{"status":"healthy","message":"Backend is running successfully"}
```

---

## Issue Encountered

Docker build initially failed due to Docker Desktop Linux engine not running on Windows.

Resolution:

* Started Docker Desktop service
* Verified daemon using `docker version`

This highlights the importance of validating container runtime availability before debugging application code.
