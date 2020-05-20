# aerospike-client-rest-kubernetes
An Aerospike REST client Helm chart for Kubernetes

## Installation
```
helm install --set config.hostname=<aerospike_hostname> rest ./aerospike-rest-client
```

To set database configuration:
* --set config.hostname=some_hostname
* --set config.port=some_port
* --set config.user=some_username
* --set config.password=some_password
* --set config.clusterName=some_clusterName