# Docker Lab Guide - Camera Stream

## Purpose

Lab 04 packages the Camera Stream service as a Docker image so another machine can run the same API and Newman checks.

## Build And Run

```bash
docker build -t fit4110/camera-stream:lab04 .
docker run --rm --name fit4110-camera-lab04 -p 8000:8000 --env-file .env.example fit4110/camera-stream:lab04
```

## App Command

```Dockerfile
CMD ["uvicorn", "camera_app.main:app", "--app-dir", "src", "--host", "0.0.0.0", "--port", "8000"]
```

The Dockerfile in this repo also uses a non-root user, healthcheck, `.dockerignore`, and environment variables.

## Healthcheck

```bash
curl http://localhost:8000/health
docker inspect fit4110-camera-lab04
```

## Secrets

Keep real tokens out of source code and pass local values through `.env.example` or a local `.env` file.
