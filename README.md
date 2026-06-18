# FIT4110 Lab 04 - Camera Stream Docker Packaging

This repository packages the Camera Stream service for Lab 04. The service accepts camera frames, keeps a lightweight frame history, calls a Vision service for analysis, and publishes camera events to Analytics.

## Main Artifacts

```text
Dockerfile
.dockerignore
.env.example
RUN_LOCAL.md
contracts/camera-stream.openapi.yaml
postman/collections/FIT4110_lab04_camera_docker.postman_collection.json
postman/environments/FIT4110_lab04_local.postman_environment.json
src/camera_app/main.py
reports/
```

## Local Run

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn camera_app.main:app --app-dir src --host 0.0.0.0 --port 8000
```

Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -r requirements.txt
uvicorn camera_app.main:app --app-dir src --host 0.0.0.0 --port 8000
```

## Docker Run

```bash
docker build -t fit4110/camera-stream:lab04 .
docker run --rm --name fit4110-camera-lab04 -p 8000:8000 --env-file .env.example fit4110/camera-stream:lab04
curl http://localhost:8000/health
```

## Verification

```bash
npm install
npm run lint:openapi
npm run test:local
```

The Newman reports are written to `reports/`.

## Submission Notes

- The Dockerfile runs the service as a non-root user.
- Runtime configuration is kept in `.env.example`.
- The submitted OpenAPI contract is `contracts/camera-stream.openapi.yaml`.
- The submitted Postman collection is the Camera Stream collection.
- No real secrets are committed.
