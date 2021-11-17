Database service creation with volume

1. Create a volume (nfs-volume.yaml)

This step defines the low level process and behaviour of our volume
is it a local volume ? nfs type ?

2. Claim volume (nfs-volume-claim.yaml)

Create the layer that allow any service to use the previous volume without having to care about the way this volume is managed

3. Run our database with the volume (mysql-replicaset.yaml)

Start the orchestrated containers

4. Wrap in a service (mysql-service.yaml)

Every open port in kubernetes should be used from a service

