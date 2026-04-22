To complete this task on **App Server 2**, follow these steps to prepare the files and launch the container with the required volume mapping.

### 1. Prepare the Host Directory
First, ensure the destination directory exists and copy the sample file into it. Since the container maps `/opt/itadmin` to its own `/tmp` directory, putting the file in `/opt/itadmin` on the host will make it appear inside the container.

```bash
# Create the directory if it doesn't exist
sudo mkdir -p /opt/itadmin

# Copy the sample file to the mapped host volume
sudo cp /tmp/sample.txt /opt/itadmin/
```

---

### 2. Pull the Nginx Image
Next, pull the latest Nginx image from the Docker registry.

```bash
sudo docker pull nginx:latest
```

---

### 3. Create and Run the Container
Run the container with the name `official`, mapping the host volume to the container volume. The `-d` (detached) flag ensures the container stays running in the background.

```bash
sudo docker run -d \
  --name official \
  -v /opt/itadmin:/tmp \
  nginx:latest
```



---

### 4. Verification
To ensure the task is completed correctly, you can run the following checks:

* **Check Container Status:**
    ```bash
    sudo docker ps
    ```
    *Verify that the container "official" is listed with a status of "Up".*

* **Verify File Persistence:**
    Check if the file is accessible inside the container's `/tmp` directory:
    ```bash
    sudo docker exec official ls /tmp
    ```
    *You should see `sample.txt` in the output.*

---

### Summary of Parameters Used
* **`-d`**: Runs the container in the background (detached mode).
* **`--name official`**: Assigns the specific name required by the ticket.
* **`-v /opt/itadmin:/tmp`**: Performs a bind mount, linking the host path to the container path.
* **`nginx:latest`**: Specifies the image and tag to use.