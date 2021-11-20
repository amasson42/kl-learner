1. We're creating the configmap of mongodb
Content of the mongo-config.yaml

2. Make the secrets for mongodb
Use base64 encoded string with the command `echo -n mysecret | base64`

3. Setup the mongo deployement and his service
Both setup in the file mongo-deployement.yaml

It takes values from the mongo-config configmap and mongo-secret secret.

4. Setup the webapp deployement and his service
On the same schema as the mongo db service in tthe file webapp-deployement.yaml
