To complete this specific task on App Server 2 , execute the following command:

docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/tmp/

Verification
You can verify the file was copied successfully without logging into the container by running:

docker exec ubuntu_latest ls -l /tmp/nautilus.txt.gpg

