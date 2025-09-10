# Mini E-commerce Flask App (with Docker & CI/CD)

This is a small Flask-based e-commerce demo app, packaged with Docker and a GitHub Actions CI/CD workflow.

## What is included
- Flask app (routes: home, login, signup, add to cart, cart)
- Dockerfile
- docker-compose.yml (for local testing)
- GitHub Actions workflow: `.github/workflows/ci-cd.yml`
- Kubernetes manifests: `k8s/deployment.yaml`, `k8s/service.yaml`

---

## Quick local run (without Docker)
```bash
pip install -r requirements.txt
python app.py
# open http://localhost:5000
```

## Run with Docker (local)
```bash
docker build -t myuser/mini-ecom-flask:latest .
docker run -p 5000:5000 myuser/mini-ecom-flask:latest
# open http://localhost:5000
```

## Run with docker-compose
```bash
docker-compose up --build
```

## GitHub Actions - CI/CD
1. Push this repo to GitHub (branch `main`).
2. In your repository go to _Settings → Secrets and variables → Actions_ and add:
   - `DOCKER_USERNAME` (your DockerHub username)
   - `DOCKER_PASSWORD` (DockerHub password or access token)
   - (optional) `KUBE_CONFIG` (kubeconfig content) if you want the workflow to also deploy to Kubernetes
3. The workflow builds and pushes the Docker image to DockerHub as:
   `DOCKER_USERNAME/mini-ecom-flask:latest`

## Kubernetes deployment (optional)
- Edit `k8s/deployment.yaml` and replace `your-dockerhub-username` with your DockerHub username.
- Apply manifests to your cluster:
  ```bash
  kubectl apply -f k8s/deployment.yaml
  kubectl apply -f k8s/service.yaml
  ```

## Notes & Safety
- Do **not** hard-code any secrets in code.
- In GitHub Actions, secrets are safe and not exposed in logs (unless intentionally echoed).
