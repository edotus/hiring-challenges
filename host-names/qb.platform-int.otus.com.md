---
description: This hostname is responsible to hold the "Query builder" RESTFUL API.
---

# qb.platform-int.otus.com



{% hint style="warning" %}
At the moment "Underdevelopment"
{% endhint %}

## How I find its serviceName?

The "ingress" namespace contain the configuration of all the hostnames. You can find the serviceName with this command:

```text
$ kubectl get ingress echo-ingres -o yaml
```

You can filter the serviceName with "jq":

```text
$ kubectl get ingress echo-ingress -o json | jq '.spec.rules[] | select((.host == "qb.platform-int.otus.com")) | .http.paths[].backend.serviceName'
```

### Information about the service

```text
Name:              alexander
Namespace:         default
Labels:            io.codefresh.auto-generated=86649492-d32f-4bb5-ae13-521ec799bd3d
                   io.codefresh.generated-at=1553621329048
Annotations:       <none>
Selector:          app=alexander
Type:              ClusterIP
IP:                10.100.144.43
Port:              http1  80/TCP
TargetPort:        8080/TCP
Endpoints:         172.31.76.228:8080
Session Affinity:  None
Events:            <none>
```

## Deployment configuration

```text
Name:                   alexander
Namespace:              default
CreationTimestamp:      Tue, 26 Mar 2019 12:28:48 -0500
Labels:                 app=alexander
                        io.codefresh.account.name=eearleyotus
                        io.codefresh.auto-generated=76c64ab6-fc5f-4784-a5e7-f9e2e70c2215
                        io.codefresh.generated-at=1553621328837
                        io.codefresh.pipeline.id=5c782da6510767ee4b29d9ef
                        io.codefresh.pipeline.name=otusteam-qbuildercoreapi-qbuildercoreapi
                        io.codefresh.process.id=5cab77e5eae9ca073b3cf3f4
                        io.codefresh.scm.branch=master
                        io.codefresh.scm.revision=4b3025f470b37870d55f064d340dcb4d7b56221d
Annotations:            deployment.kubernetes.io/revision=25
                        kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"extensions/v1beta1","kind":"Deployment","metadata":{"annotations":{"deployment.kubernetes.io/revision":"24"},"generation":31,"labels":{"...
Selector:               app=alexander,io.codefresh.auto-generated=76c64ab6-fc5f-4784-a5e7-f9e2e70c2215,io.codefresh.generated-at=1553621328837
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  50% max unavailable, 50% max surge
Pod Template:
  Labels:       app=alexander
                io.codefresh.auto-generated=76c64ab6-fc5f-4784-a5e7-f9e2e70c2215
                io.codefresh.generated-at=1553621328837
  Annotations:  forceRedeployUniqId=87dc673c-4270-4f7e-ab8f-1335ad566926
                forceRedeployUniqueId=1554741604991
  Containers:
   alexander:
    Image:        r.cfcr.io/eearleyotus/otusteam/qbuildercoreapi:master-4b3025f
    Port:         8080/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   alexander-cc945f4cd (1/1 replicas created)
Events:          <none>
```

