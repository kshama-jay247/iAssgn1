# Assignment 2 – Two Containers Communicating via Docker Network

## Goal
Deploy two Docker containers:
- A **web container** (Nginx) serving a static web page
- An **API container** returning a simple text response

Both containers communicate with each other using a **custom Docker network**.

---

## Components Used

### 1. Web Container
- Built using `nginx:alpine`
- Serves a static HTML page
- Proxies `/api` requests to the API container
- Exposed to the host machine on port **8080**

### 2. API Container
- Uses the prebuilt image **`hashicorp/http-echo`**
- Returns a simple response:  
  `"Hello from API"`
- Runs only inside the Docker network (not exposed to host)

---

## Files in This Folder

- `Dockerfile` – builds the custom Nginx web container
- `index.html` – static web page with a button to call the API
- `nginx.conf` – Nginx configuration to proxy `/api` requests

---

```bash
docker network create webnet

```

## Steps to follow

### To create an image

```bash
docker build -t web_image .

```

### To run the API container on that network

```bash
docker run -d --name api --network webnet hashicorp/http-echo -text="Hello from API"

```

### To create a container and run it on port 8080

```bash
docker run -d --name web --network webnet -p 8080:80 web_image

```

## Output 
![Static Web Page](imge.png)