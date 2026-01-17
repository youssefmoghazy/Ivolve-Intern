# Lab 7: Docker Volume and Bind Mount with Nginx

This lab demonstrates how to use **Docker Volumes** and **Bind Mounts** with an **Nginx** container to persist logs and serve static content from the host machine.

---

## 📌 Objectives

* Create a Docker volume to persist Nginx logs
* Use a bind mount to serve custom HTML content from the host
* Verify live changes without restarting the container
* Inspect Docker volume data
* Clean up volumes and containers

---

## 🧰 Prerequisites

* Docker installed
* Basic Linux command knowledge

Verify Docker:

```bash
docker --version
```

---

## 1️⃣ Create Docker Volume for Nginx Logs

Create a volume named **nginx_logs**:

```bash
docker volume create nginx_logs
```

Verify the volume exists:

```bash
docker volume ls
```

Inspect volume to see default path:

```bash
docker volume inspect nginx_logs
```

> Docker stores volumes by default under:
> `/var/lib/docker/volumes/`

---

## 2️⃣ Create Bind Mount Directory on Host

Create directories for bind mount:

```bash
mkdir -p nginx-bind/html
```

---

## 3️⃣ Create Custom index.html File

Create the HTML file:

```bash
nano nginx-bind/html/index.html
```

Add the following content:

```html
Hello from Bind Mount
```

Save and exit.

---

## 4️⃣ Run Nginx Container with Volume & Bind Mount

Run the Nginx container using:

```bash
docker run -d \
  -p 8080:80 \
  -v nginx_logs:/var/log/nginx \
  -v $(pwd)/nginx-bind/html:/usr/share/nginx/html \
  --name nginx-lab \
  nginx
```

### 🔍 Explanation

* `nginx_logs:/var/log/nginx` → Docker Volume for logs
* `$(pwd)/nginx-bind/html:/usr/share/nginx/html` → Bind mount for HTML

---

## 5️⃣ Verify Nginx Page

From your local machine, run:

```bash
curl http://localhost:8080
```

Expected output:

```text
Hello from Bind Mount
```

---

## 6️⃣ Modify HTML File and Verify Live Update

Edit the file on your host machine:

```bash
nano nginx-bind/html/index.html
```

Change content to:

```html
Hello from Updated Bind Mount
```

Save the file, then run:

```bash
curl http://localhost:8080
```

✅ The updated content should appear **without restarting the container**.

---

## 7️⃣ Stop Container and Delete Volume

Stop and remove the container:

```bash
docker stop nginx-lab
docker rm nginx-lab
```

Delete the volume:

```bash
docker volume rm nginx_logs
```

Verify deletion:

```bash
docker volume ls
```

---

## 🧠 Key Concepts

* **Docker Volume** persists data managed by Docker
* **Bind Mount** links a host directory directly to the container
* Bind mounts allow real-time updates
* Volumes are ideal for persistent application data like logs

---

## ✅ Lab Completed

You have successfully used Docker volumes and bind mounts with Nginx to persist logs and serve live content from the host machine 🚀


