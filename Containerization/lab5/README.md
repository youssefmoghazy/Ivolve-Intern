# Lab 5: Multi-Stage Build for an Application (Java – Maven)

This lab demonstrates how to use a **multi-stage Docker build** to containerize a Java application using **Maven** for building and **Java runtime** for execution.

> ⚠️ Note: Although the lab title mentions Node.js, the provided application is a **Java Spring Boot** project built with **Maven**.

---

## 📌 Objectives

* Clone the application source code
* Write a **multi-stage Dockerfile**
* Build the application using Maven inside Docker
* Run the application using a lightweight Java image
* Reduce final image size
* Test and clean up containers

---

## 🧰 Prerequisites

Make sure you have installed:

* Git
* Docker

Verify Docker:

```bash
docker --version
```

---

## 1️⃣ Clone the Application Code

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
```

---

## 2️⃣ Write Multi-Stage Dockerfile

Create a file named **Dockerfile** in the project root:

```dockerfile
# ============================
# Stage 1: Build Stage
# ============================
FROM maven:3.9.6-eclipse-temurin-17 AS build

WORKDIR /build

# Copy pom.xml first for dependency caching
COPY pom.xml .
RUN mvn dependency:go-offline

# Copy application source code
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests

# ============================
# Stage 2: Runtime Stage
# ============================
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

# Copy JAR from build stage
COPY --from=build /build/target/demo-0.0.1-SNAPSHOT.jar app.jar

EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

## 3️⃣ Build app3 Docker Image

```bash
docker build -t app3 .
```

Check the image size:

```bash
docker images
```

📝 You will notice that the multi-stage image size is significantly smaller than a single-stage image.

---

## 4️⃣ Run Container from app3 Image

```bash
docker run -d -p 8081:8080 --name container3 app3
```

Verify the container is running:

```bash
docker ps
```

---

## 5️⃣ Test the Application

Using browser:

```
http://localhost:8081
```

Or using curl:

```bash
curl http://localhost:8081
```

You should receive a response from the Spring Boot application.

---

## 6️⃣ Stop and Delete the Container

Stop the container:

```bash
docker stop container3
```

Remove the container:

```bash
docker rm container3
```

(Optional) Remove the image:

```bash
docker rmi app3
```

---

## 🧠 Why Multi-Stage Build?

* Keeps build tools (Maven) out of production image
* Reduces final image size
* Improves security
* Follows industry best practices

---

## ✅ Lab Completed

You have successfully built and run a Java application using a **multi-stage Docker build** 🚀

