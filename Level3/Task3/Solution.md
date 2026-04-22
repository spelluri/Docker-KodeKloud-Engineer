To set up the Nginx container on **App Server 1** according to the ticket requirements, follow these steps:

---

## 1. Pull the Specific Image
First, fetch the required image from the Docker registry. Using the specific `alpine-perl` tag ensures you have the correct version requested by the team.

```bash
sudo docker pull nginx:alpine-perl
```

---

## 2. Create and Run the Container
Run the container in the background (detached mode) with the specified name and port mapping.

```bash
sudo docker run -d \
  --name ecommerce \
  -p 8087:80 \
  nginx:alpine-perl
```

---

## 3. Verification
After running the command, you should verify that the container is active and accessible.

* **Check Container Status:**
    ```bash
    sudo docker ps
    ```
    *Verify that the name **ecommerce** is present and the status is **Up**.*

* **Verify Port Mapping:**
    In the `docker ps` output, ensure you see `0.0.0.0:8087->80/tcp`. This confirms that traffic hitting the host on port **8087** is correctly routed to the container's port **80**.

* **Test Web Response:**
    ```bash
    curl -I http://localhost:8087
    ```
    *A successful setup will return an `HTTP/1.1 200 OK` header from the Nginx server.*

---

### Parameter Summary
| Parameter | Description |
| :--- | :--- |
| **`-d`** | Runs the container in **detached mode** so it stays running in the background. |
| **`--name ecommerce`** | Assigns the specific name required by the ticket. |
| **`-p 8087:80`** | Maps the **host port (8087)** to the **container port (80)**. |
| **`nginx:alpine-perl`** | Specifies the exact image and tag to be used. |