# Lab 8: Custom Docker Network for Microservices (Python – Flask)

This lab demonstrates how to build and run **frontend** and **backend** microservices using **Python Flask**, containerize them with **Docker**, and enable secure communication between them using a **custom Docker network**.

The goal is to understand how Docker networking allows containers to discover and communicate with each other using service names instead of IP addresses.

## 📁 Project Structure

```text
lab8-docker-network/
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
├── frontend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
└── README.md
```

---

##  Step 1:Backend Flask Application


### `backend/Dockerfile`

```dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

EXPOSE 5000

CMD ["python", "app.py"]
```

---

##  Step 2: Frontend Flask Application

### `frontend/Dockerfile`

```dockerfile
FROM python:3.10-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY app.py .

EXPOSE 5001

CMD ["python", "app.py"]
```

---

## 🏗️ Step 3: Build Docker Images

From the project root directory:

```bash
docker build -t backend-image ./backend
docker build -t frontend-image ./frontend
```

Verify images:

```bash
docker images
```

---

## 🌐 Step 4 : Create a Custom Docker Network

Create a bridge network:

```bash
docker network create ivolve-network
```

Verify network creation:

```bash
docker network ls
```

---

## ▶️ Step 5: Run Containers on the Custom Network

### Run Backend Container

```bash
docker run -d \
  --name backend \
  --network ivolve-network\
  backend-image
```

### Run Frontend Container

```bash
docker run -d \
  --name frontend \
  --network ivolve-network \
  -p 5001:5001 \
  frontend-image
```

---

## 🔍 Step 6: Test Container Communication

Open a browser or use `curl`:

```bash
curl http://localhost:5001
```

Expected output:

```text
Frontend received: Hello from Backend Service
```

This confirms that:

* Both containers are on the same custom network
* Docker DNS resolves the backend container by name
* Frontend can successfully communicate with backend

---

## 🧪 Step 7: Inspect the Network (Optional)

```bash
docker network inspect microservices-net
```

This shows connected containers and assigned IP addresses.

---

## 🧹 Step 8: Clean Up

Stop and remove containers:

```bash
docker stop frontend backend
docker rm frontend backend
```

Remove images:

```bash
docker rmi frontend-image backend-image
```

Remove the custom network:

```bash
docker network rm microservices-net
```

---

🎉 **Lab Complete!** You have successfully built and networked Flask-based microservices using Docker.

