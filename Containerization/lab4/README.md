# Lab 4: Run Java Spring Boot App in a Container

This lab demonstrates how to containerize and run a **Java Spring Boot** application using **Docker**.

---

## 📌 Objectives

* Clone a Spring Boot application
* Build the application
* Write a Dockerfile using **Java 17**
* Build and run a Docker image
* Test the running application
* Stop and remove the container

---

## 🧰 Prerequisites

Make sure you have the following installed:

* Git
* Java 17
* Maven
* Docker

Verify installations:

```bash
java -version
mvn -version
docker --version
```

---

## 1️⃣ Clone the Application Code

Clone the repository from GitHub:

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git
cd Docker-1
```

---

## 2️⃣ Build the Application

Use Maven to build the Spring Boot application and generate the JAR file:

```bash
mvn clean package
```

After a successful build, the JAR file will be created at:

```text
target/demo-0.0.1-SNAPSHOT.jar
```

---

## 3️⃣ Write the Dockerfile

Create a file named **Dockerfile** in the project root directory:

```dockerfile
# Use Java 17 base image
FROM eclipse-temurin:17-jdk-alpine

# Create and set working directory
WORKDIR /app

# Copy the JAR file into the container
COPY target/demo-0.0.1-SNAPSHOT.jar app.jar

# Expose application port
EXPOSE 8080

# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
```

### 🔍 Explanation

* **FROM**: Uses a lightweight Java 17 image
* **WORKDIR**: Sets `/app` as the working directory
* **COPY**: Copies the built JAR into the container
* **EXPOSE**: Opens port 8080
* **ENTRYPOINT**: Runs the Spring Boot application

---

## 4️⃣ Build app2 Docker Image

Build the Docker image and name it **app2**:

```bash
docker build -t app2 .
```

Check the image size:

```bash
docker images
```

---

## 5️⃣ Run Container from app2 Image

Run a container named **container2** from the image:

```bash
docker run -d -p 8080:8080 --name container2 app2
```

Verify the container is running:

```bash
docker ps
```

---

## 6️⃣ Test the Application

Open your browser or use curl:

```text
http://localhost:8080
```

Or:

```bash
curl http://localhost:8080
```

You should see the Spring Boot application response.

---

## 7️⃣ Stop and Delete the Container

Stop the running container:

```bash
docker stop container2
```

Remove the container:

```bash
docker rm container2
```

(Optional) Remove the image:

```bash
docker rmi app2
```

---

## ✅ Lab Completed

You have successfully built, containerized, and run a Java Spring Boot application using Docker 🚀

