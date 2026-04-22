To set up the Docker network according to the ticket specifications, you will need to run the following command on App Server 1 .

The Command
Run this command in your terminal to create the network with the specific driver, subnet, and IP range:

docker network create \
  --driver bridge \
  --subnet 10.10.1.0/24 \
  --ip-range 10.10.1.0/24 \
  blog

  Verification
Once executed, you can verify that the network was created correctly by checking the network list and then inspecting the details:

1. List all networks:
docker network ls

Look for "blog" in the NAME column and "bridge" in the DRIVER column.

2. Inspect the configuration:

docker network inspect blog

Confirm that the Subnetand IPRangematch 10.10.1.0/24.

