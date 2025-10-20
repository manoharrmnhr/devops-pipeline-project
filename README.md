# 🚀 DevOps Pipeline Project

This project demonstrates a **complete CI/CD pipeline** for a simple Node.js web application using **Docker** and **GitHub Actions**.  
Whenever you push changes to the `main` branch, the pipeline automatically builds, tests, and pushes the Docker image to Docker Hub.

---

## 🧱 Tech Stack

- **Backend:** Node.js + Express  
- **Containerization:** Docker  
- **CI/CD Automation:** GitHub Actions  
- **Image Registry:** Docker Hub

---

## 🛠️ Project Structure


- `server.js` → Node.js application file  
- `Dockerfile` → Instructions to build the container image  
- `.github/workflows/main.yml` → GitHub Actions CI/CD workflow  

---

## ⚡ How It Works

1. **Code Push:** Developer pushes changes to GitHub.  
2. **Pipeline Triggered:** GitHub Actions workflow starts automatically.  
3. **Build & Test:**  
   - Installs dependencies  
   - Runs tests (if any)  
4. **Docker Image Build:** Creates a new image from the Dockerfile.  
5. **Push to Docker Hub:** Authenticates using GitHub Secrets and pushes the image.

---

## 🐳 Run Locally with Docker

```bash
# Build the Docker image
docker build -t nodejs-demo-app .

# Run the container
docker run -p 9090:9090 nodejs-demo-app

on:
  push:
    branches: [ "main" ]

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install
      - run: npm test
      - uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
      - uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ${{ secrets.DOCKER_USERNAME }}/devops-pipeline-project:latest


---

Would you like me to include **badges** (e.g., “Build Passing” or “Docker Image”) at the top of this README for a more professional look? 🏷️✨

