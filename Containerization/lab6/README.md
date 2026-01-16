# Lab 6: Managing Docker Environment Variables Across Build and Runtime

This lab demonstrates how to manage **Docker environment variables** for a Python Flask application at build time, run time, and via environment files.

---

## 📌 Objectives

* Clone the application code
* Write a Dockerfile for a Flask app
* Build the Docker image
* Run containers using different methods for environment variables
* Understand differences between build-time, run-time, and env-file variables

---

## 🧰 Prerequisites

* Git
* Docker
* Basic knowledge of Flask

Verify Docker:

```bash
docker --version
```

---

## 1️⃣ Clone the Application Code

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-3.git
cd Docker-3
```

---

## 2️⃣ Write Dockerfile

Create a file named **Dockerfile** in the project root:

```dockerfile
# Base Python image
FROM python:3.12-alpine

# Install Flask
RUN pip3 install flask

# Set environment variables at build time (production)
ENV APP_MODE=production
ENV APP_REGION=canada-west

# Set working directory
WORKDIR /app

# Copy application code
COPY app.py .

# Expose port 8080
EXPOSE 8080

# Run the Flask application
CMD ["python3", "app.py"]
```

### 🔍 Notes

* `ENV` sets variables **inside the image** (build-time defaults)
* `CMD` runs the app inside the container

---

## 3️⃣ Build Docker Image

```bash
docker build -t python-env-app .
```

Check the image:

```bash
docker images
```

---

## 4️⃣ Run Containers with Different Env Variables

### i. Set environment variables in the `docker run` command (development, us-east)

```bash
docker run -d -p 8081:8080 \
  -e APP_MODE=development \
  -e APP_REGION=us-east \
  --name app_dev python-env-app
```

Test:

```bash
curl http://localhost:8081
```

### ii. Use an environment file (staging, us-west)

Create a file named `app_env_file.env`:

```
APP_MODE=staging
APP_REGION=us-west
```

Run container with env file:

```bash
docker run -d -p 8082:8080 --env-file app_env_file.env --name app_staging python-env-app
```

Test:

```bash
curl http://localhost:8082
```

### iii. Use environment variables set in Dockerfile (production, canada-west)

```bash
docker run -d -p 8083:8080 --name app_prod python-env-app
```

Test:

```bash
curl http://localhost:8083
```

> The container uses the defaults specified in the Dockerfile

---

## 5️⃣ Stop and Delete Containers

```bash
docker stop app_dev app_staging app_prod
```

```bash
docker rm app_dev app_staging app_prod
```

---

**Key Points:**

* Environment variables can be set at build-time, run-time, or using env-files
* Run-time variables override Dockerfile defaults
* Env-files provide a convenient way to manage multiple variables

---

## ✅ Lab Completed

You have successfully managed environment variables for a Python Flask application using Docker across build-time, run-time, and env-file configurations.

