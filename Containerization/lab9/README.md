# Lab 9: Containerized Node.js and MySQL Stack Using Docker Compose

This lab demonstrates how to containerize a **Node.js application** with a **MySQL database** using **Docker Compose**. You will build the application image, configure service communication, persist database data using volumes, verify application health endpoints, and push the image to **Docker Hub**.

---

##  Step 1: Clone the Application Repository

Clone the provided Node.js application:

```bash
git clone https://github.com/Ibrahim-Adel15/kubernets-app.git
cd kubernets-app
```
---

##  Step 2: Review Dockerfile

Ensure the application contains a `Dockerfile` similar to the following:

```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

---

##  Step 3: Create docker-compose.yml

Create a file named `docker-compose.yml` in the project root directory.

```yaml
version: "3.9"

services:
  app:
    build: .
    container_name: node-app
    ports:
      - "3000:3000"
    environment:
      DB_HOST: db
      DB_USER: root
      DB_PASSWORD: rootpassword
    depends_on:
      - db

  db:
    image: mysql:8.0
    container_name: mysql-db
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: ivolve
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

---

##  Step 4: Start the Application Stack

Build and start the containers:

```bash
docker compose up -d --build
```

Check running containers:

```bash
docker compose ps
```

---

##  Step 5: Verify Application Functionality

### 1️⃣ Verify Application is Running

Open your browser:

```text
http://localhost:3000
```

The application should load successfully.

---

### 2️⃣ Verify Health Endpoint

```bash
curl http://localhost:3000/health
```

Expected response:

```json
{"status":"healthy"}
```

---

### 3️⃣ Verify Readiness Endpoint

```bash
curl http://localhost:3000/ready
```

Expected response:

```json
{"status":"ready"}
```

---

### 4️⃣ Verify Application Logs

Access the logs directory inside the container:

```bash
docker exec -it node-app ls /app/logs
```

View logs:

```bash
docker exec -it node-app cat /app/logs/access.log
```

---

##  Step 6: Verify Database Persistence

Stop and restart containers:

```bash
docker compose down
docker compose up -d
```

The MySQL data remains intact because it is stored in the `db_data` volume.

---

##  Step 7: Push Docker Image to Docker Hub

### 1️⃣ Login to Docker Hub

```bash
docker login
```

### 2️⃣ Tag the Image

Replace `your_dockerhub_username` with your Docker Hub username:

```bash
docker tag kubernets-app-app your_dockerhub_username/node-mysql-app:latest
```

### 3️⃣ Push the Image

```bash
docker push your_dockerhub_username/node-mysql-app:latest
```

---

##  Step 8: Clean Up

Stop containers and remove resources:

```bash
docker compose down -v
```

---

🎉 **Lab Complete!** You have successfully containerized a Node.js and MySQL application using Docker Compose.

