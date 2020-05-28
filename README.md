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

To change default number of replicas:
* --set replicaCount=3


### Configurations

| Parameter | Description| Default Value |
|:----------|:----------:|:-------------:|
| `replicaCount` | Number of replicas for the Aerospike REST client deployment | `1` |
| `image.repository` | Aerospike REST client docker image repository | `aerospike/aerospike-client-rest` |
| `image.tag` | Aerospike REST client docker image tag | `latest` |
| `config.hostname` | Aerospike cluster Seed IP address to connect to | `127.0.0.1` |
| `config.port` | Aerospike cluster Seed Port | `3000` |
| `config.user` | Username for access control to connect to the aerospike cluster | `""` |
| `config.password` | Password for access control to connect to the aerospike cluster | `""` |
| `config.clusterName` | Cluster name defined for the aerospike cluster | `""` |
| `serviceAccount.create` | Create and use a serviceAccount for the deployment | `true` |
| `serviceAccount.annotations` | Annotations for the serviceAccount resource | `{} (nil)` |
| `serviceAccount.name` | ServiceAccount name whether to be created or already exists | `true` |
| `podSecurityContext` | Pod security context | `{} (nil)` |
| `securityContext` | Container security context | `{} (nil)` |
| `containerPort` | Aerospike REST client deployment container port | `8080` |
| `service.type` | Type of service to access REST client deployment | `ClusterIP` |
| `service.port` | Port for the service to access REST client deployment | `8080` |
| `ingress.enabled` | Enable Ingress resource | `false` |
| `ingress.annotations` | Annotations for Ingress resource | `{} (nil)` |
| `ingress.rules` | Rules for Ingress resource | `[] (nil)` |
| `ingress.tls` | TLS configuration for Ingress resource | `[] (nil)` |
| `resources` | Resources and Limits for REST client Deployment | `{} (nil)` |
| `nodeSelector` | Specify node selectors labels for Pod scheduling | `{} (nil)` |
| `tolerations` | Define tolerations and taints for Pod scheduling and execution | `[] (nil)` |
| `affinity` | Define pod and node affinity and antiAffinity | `{} (nil)` |
