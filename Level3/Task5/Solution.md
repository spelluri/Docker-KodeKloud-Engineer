To host the static website content on **App Server 2** using Docker Compose, follow these steps to set up the configuration file and launch the service.

---

### 1. Create the Project Directory
Since the ticket specifies the path `/opt/docker/docker-compose.yml`, you first need to make sure that directory exists.

```bash
sudo mkdir -p /opt/docker
cd /opt/docker
```

---

### 2. Create the Docker Compose File
Use a text editor (like `vi`, `vim`, or `nano`) to create the file.

```bash
sudo vi /opt/docker/docker-compose.yml
```

**Paste the following content into the file:**

```yaml
version: '3.8'

services:
  web-server:
    image: httpd:latest
    container_name: httpd
    ports:
      - "8086:80"
    volumes:
      - /opt/security:/usr/local/apache2/htdocs
    restart: always
```

> **Note on the Config:** > * **`container_name: httpd`**: This ensures the container itself is named exactly as requested, regardless of the service name.
> * **`volumes`**: This maps the existing static content from the host into the default Apache document root.

---

### 3. Deploy the Container
Navigate to the directory (if you aren't already there) and start the container in detached mode.

```bash
cd /opt/docker
sudo docker compose up -d
```
*(If your system uses the older version of Compose, the command might be `sudo docker-compose up -d`.)*

---

### 4. Verification
To ensure everything is mapped correctly without touching the data, run these checks:

* **Check the Container Name & Ports:**
  ```bash
  sudo docker ps
  ```
  Verify that the name is **httpd** and the ports show **0.0.0.0:8086->80/tcp**.

* **Verify the Volume Mount:**
  ```bash
  sudo docker inspect httpd | grep -A 10 "Mounts"
  ```
  Confirm the `Source` is `/opt/security` and the `Destination` is `/usr/local/apache2/htdocs`.

* **Test the Website:**
  ```bash
  curl -I http://localhost:8086
  ```
  You should receive an `HTTP/1.1 200 OK` response.



---

### Troubleshooting Tip
If the container fails to start, check the logs using `sudo docker logs httpd`. Since you aren't allowed to modify data in `/opt/security`, ensure the Docker daemon has read permissions for that directory so it can serve the files.

**How is the migration looking so far—are there any other servers in the Stratos DC that need similar setups?**