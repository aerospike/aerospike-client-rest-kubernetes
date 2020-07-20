# Helm chart for Aerospike REST Client on Kubernetes

Implements Aerospike REST client deployment on Kubernetes

## Usage

### Add Aerospike repository

```
helm repo add aerospike https://aerospike.github.io/aerospike-kubernetes-enterprise
```

### Install the chart

```
helm install rest-client aerospike/aerospike-rest-client --set config.hostname=<aerospike_hostname>
```

## Configuration


### Connect to Aerospike cluster

#### Specify aerospike cluster seed IP or hostname and port

```
helm install rest-client aerospike/aerospike-rest-client \
            --set config.hostname=demo-aerospike-enterprise \
            --set config.port=3000
```

#### Specify username and password (for security enabled clusters)

```
helm install rest-client aerospike/aerospike-rest-client \
            --set config.hostname=demo-aerospike-enterprise \
            --set config.port=3000 \
            --set config.user=superman \
            --set config.password=krypton
```

#### Specify cluster name (if applicable)
```
--set config.clusterName=demo-aerospike-enterprise
```


### Expose REST client deployment

#### Using NodePort type service

Aerospike REST client can be exposed for external access using NodePort type services.

Set `service.type=NodePort` to expose REST client via a `NodePort`.

Applications can access REST client endpoint at `<K8sNodeIP>:<NodePort>`.

#### Using LoadBalancer type service

Aerospike REST client can be exposed for external access using Load balancers.

Set `service.type=LoadBalancer` to expose REST client via a network load balancer.

Applications can access REST client endpoint at `<LoadBalancerIP>:<LoadBalancerPort>`

#### Using Ingress

Aerospike REST client can be exposed for external access using ingress.

- Set `ingress.enabled=true`,
- Specify `ingress.annotations`, `ingress.rules` and `ingress.tls` configuration.

For example (using `nginx` controller),
```yaml
# Ingress resource settings
ingress:
  enabled: true
  annotations:
    kubernetes.io/ingress.class: nginx
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
  rules: []
    - paths:
        - '/'
      # host: rest.aerospike.com
  tls: []
  # - secretName: rest-client-tls
  #   hosts:
  #   - rest.aerospike.com
```

Applications can access REST client endpoint at the specified url (or `host`) in the `rules` or at the external IP of ingress controller (loadbalancer).


## Configuration parameters and default values

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
| `config.requireAuthentication` | Require the Basic Authentication on each request | `false` |
| `config.poolSize` | Represents the max size of the clients LRU cache | `16` |
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
