# 🐳 Docker Cheat Sheet & Core Concepts

A practical guide to essential Docker commands covering lifecycle management, port mapping, environment variables, and working with remote registries.

---

## 📌 1. Basic Container Lifecycle

Commands to build, run, inspect, and stop your containers.

* **Build an image from a Dockerfile:**
  ```bash
  docker build -t <image-name>:<tag> .
  ```
  *Example:* `docker build -t my-app:1.0 .`

* **Run a container in the foreground (Attached Mode):**
  ```bash
  docker run -it <image-name>
  ```
  *(Locks your terminal and shows logs in real-time. Stop it using `Ctrl + C`)*

* **Run a container in the background (Detached Mode):**
  ```bash
  docker run -d <image-name>
  ```

* **List running containers:**
  ```bash
  docker ps
  ```

* **Stop a background container:**
  ```bash
  docker stop <container-id-or-name>
  ```

---

## 🔌 2. Port Mapping (`-p`)

Containers live in isolated networks. To access a web server inside a container from your laptop's browser, you must bridge the ports using the `-p` flag.

```text
       ┌── Host Port: The port you type into your browser (e.g., localhost:8080)
       │
       ▼
-p   8080  :  8000
               ▲
               │
               └── Container Port: The exact port your app listens to internally
```

### Important Rule:
Your application code **must** listen on host `0.0.0.0` (all network interfaces) inside the container, not `127.0.0.1` (localhost).

* **Example Command:**
  ```bash
  docker run -d -p 8080:8000 my-app
  ```
  *Access it at:* `http://localhost:8080`

---

## 🌿 3. Injecting Environment Variables (`-e`)

You can pass environment variables dynamically into your container at runtime without hardcoding them into your source files or images.

* **Pass a single variable:**
  ```bash
  docker run -d -e PORT=8000 -p 8000:8000 my-app
  ```

* **Pass multiple variables:**
  ```bash
  docker run -d -e PORT=8000 -e NODE_ENV=production -p 8000:8000 my-app
  ```

---

## 🚀 4. Pulling and Pushing Images

Interacting with remote registries like Docker Hub.

* **Log into Docker Hub:**
  ```bash
  docker login
  ```

* **Pull an image from a registry:**
  ```bash
  docker pull <username>/<repository>:<tag>
  ```
  *Example:* `docker pull shlk69/test-image:latest`


* **Push an image to a registry:**
  ```bash
  docker push <username>/<repository>:<tag>
  ```
  *Example:* `docker push shlk69/test-image:latest`

---
