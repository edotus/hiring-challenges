---
description: This hostname is responsible for the backend of Otus application.
---

# napi.platform-int.otus.com

## How I find its serviceName?

The "ingress" namespace contain the configuration of all the hostnames. You can find the serviceName with this command:

```text
$ kubectl get ingress echo-ingres -o yaml
```

You can filter the serviceName with "jq":

```text
$ kubectl get ingress echo-ingress -o json | jq '.spec.rules[] | select((.host == "napi.platform-int.otus.com")) | .http.paths[].backend.serviceName'
```

### Information about the service

```text
Name:              node-api
Namespace:         default
Labels:            io.codefresh.auto-generated=18e5ce2b-3c8c-4699-bf43-80ee6d86ebe9
                   io.codefresh.generated-at=1554227825702
Annotations:       <none>
Selector:          app=node-api
Type:              ClusterIP
IP:                10.100.179.224
Port:              http1  3036/TCP
TargetPort:        3036/TCP
Endpoints:         172.31.78.21:3036,172.31.89.137:3036
Session Affinity:  None
Events:            <none>
```

## Deployment configuration

```text
Name:                   node-api
Namespace:              default
Replicas:               2 desired | 2 updated | 2 total | 2 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  50% max unavailable, 50% max surge
Pod Template:
  Labels:       app=node-api
                io.codefresh.auto-generated=261b1314-a81d-4346-923b-dd30d1568395
                io.codefresh.generated-at=1554227825266
  Annotations:  forceRedeployUniqId=24c10961-10d0-4a81-b1c8-edf808444b0f
                forceRedeployUniqueId=1554652533683
  Containers:
   node-api:
    Image:        r.cfcr.io/eearleyotus/otus/node-internal-api:master-0710490
    Port:         3036/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   node-api-96bb4cd6c (2/2 replicas created)
Events:          <none>
```



