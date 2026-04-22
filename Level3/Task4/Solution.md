To move the Docker image from **App Server 1** to **App Server 3**, you will use the `docker save` and `docker load` workflow. This is the standard way to migrate images without using a central registry.

---

### Step 1: Prepare and Save on App Server 1
First, ensure the Docker service is running and export the image into a compressed archive.

```bash
# Ensure Docker is running
sudo systemctl start docker

# Save the image to a .tar file
sudo docker save -o ecommerce_datacenter.tar ecommerce:datacenter
```

---

### Step 2: Transfer the Archive to App Server 3
Use `scp` (Secure Copy) to send the file across the network to the `/tmp` directory of App Server 3. 

*Note: Replace `[user]` and `[app_server_3_ip]` with the actual credentials for your environment.*

```bash
scp ecommerce_datacenter.tar [user]@[app_server_3_ip]:/tmp/
```

---

### Step 3: Load the Image on App Server 3
Log into **App Server 3** to finalize the process. You must ensure the Docker service is active here as well before loading the archive.

```bash
# Ensure Docker is running
sudo systemctl start docker

# Load the image from the archive
sudo docker load -i /tmp/ecommerce_datacenter.tar
```



---

### Step 4: Verification
Run the following command on **App Server 3** to confirm the image is present with the correct repository and tag:

```bash
sudo docker images
```

**Expected Output:**
You should see a row matching this:
`REPOSITORY: ecommerce` | `TAG: datacenter`

---

### Summary of Commands
* **`docker save`**: Packages the image layers and metadata into a single tarball.
* **`scp`**: A standard utility for securely transferring files between hosts.
* **`docker load`**: Reconstitutes the image from the tarball back into the local Docker engine's storage.