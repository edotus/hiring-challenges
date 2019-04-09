---
description: This hostname is responsible for the front-end of Otus application.
---

# stage-fe.platform-int.otus.com

## How I find its serviceName?

The "ingress" namespace contain the configuration of all the hostnames. You can find the serviceName with this command:

```text
$ kubectl get ingress echo-ingres -o yaml
```

You can filter the serviceName with "jq":

```text
$ kubectl get ingress echo-ingress -o json | jq '.spec.rules[] | select((.host == "stage-fe.platform-int.otus.com")) | .http.paths[].backend.serviceName'
```

### Information about the service

```text
Name:              ci-staging-fe
Namespace:         default
Labels:            io.codefresh.auto-generated=4f264c3c-f6b8-42b1-bd20-7507b3171618
                   io.codefresh.generated-at=1554166220020
Annotations:       <none>
Selector:          app=ci-staging-fe
Type:              ClusterIP
IP:                10.100.149.30
Port:              http1  80/TCP
TargetPort:        8080/TCP
Endpoints:         172.31.14.219:8080,172.31.65.213:8080,172.31.78.139:8080 + 2 more...
Session Affinity:  None
Events:            <none>
```

## Deployment configuration

```text
Name:                   ci-staging-fe
Namespace:              default
CreationTimestamp:      Mon, 01 Apr 2019 19:50:20 -0500
Labels:                 app=ci-staging-fe
                        io.codefresh.account.name=eearleyotus
                        io.codefresh.auto-generated=071a3853-d92b-4190-9da9-0d6392f8b585
                        io.codefresh.generated-at=1554166220062
                        io.codefresh.pipeline.id=5c86862934520463544410b7
                        io.codefresh.pipeline.name=bitbucket-bitbucket-otusteam-source-code-source-code
                        io.codefresh.process.id=5caa15e635b49bdb152f77d8
                        io.codefresh.scm.branch=master
                        io.codefresh.scm.revision=0710490e71d29cf7ad2d1f2934b862c3a9ba715a
Annotations:            deployment.kubernetes.io/revision=27
                        kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"extensions/v1beta1","kind":"Deployment","metadata":{"annotations":{"deployment.kubernetes.io/revision":"26"},"generation":28,"labels":{"...
Selector:               app=ci-staging-fe,io.codefresh.auto-generated=071a3853-d92b-4190-9da9-0d6392f8b585,io.codefresh.generated-at=1554166220062
Replicas:               5 desired | 5 updated | 5 total | 5 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  50% max unavailable, 50% max surge
Pod Template:
  Labels:       app=ci-staging-fe
                io.codefresh.auto-generated=071a3853-d92b-4190-9da9-0d6392f8b585
                io.codefresh.generated-at=1554166220062
  Annotations:  forceRedeployUniqId=672b37d9-9d91-4da4-babe-c494c6611d2c
                forceRedeployUniqueId=1554652326299
  Containers:
   ci-staging-fe:
    Image:        r.cfcr.io/eearleyotus/otusteam/fe:master-0710490
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
NewReplicaSet:   ci-staging-fe-7d4b69d485 (5/5 replicas created)
Events:          <none>
```

