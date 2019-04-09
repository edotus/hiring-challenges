---
description: >-
  This hostname is responsible for the legacy PHP application. A lot of
  functionalities are handle by this legacy application.
---

# papi.platform-int.otus.com

## How I find its serviceName?

The "ingress" namespace contain the configuration of all the hostnames. You can find the serviceName with this command:

```text
$ kubectl get ingress echo-ingres -o yaml
```

You can filter the serviceName with "jq":

```text
$ kubectl get ingress echo-ingress -o json | jq '.spec.rules[] | select((.host == "papi.platform-int.otus.com")) | .http.paths[].backend.serviceName'
```

### Information about the service

```text
Name:              php-api
Namespace:         default
Labels:            io.codefresh.auto-generated=5978c3d2-a813-4e0b-ba20-2d8472db91b8
                   io.codefresh.generated-at=1554234705284
Annotations:       <none>
Selector:          app=php-api
Type:              ClusterIP
IP:                10.100.128.155
Port:              http1  80/TCP
TargetPort:        80/TCP
Endpoints:         172.31.87.162:80
Session Affinity:  None
Events:            <none>
```

## Deployment configuration

```text
Name:                   php-api
Namespace:              default
CreationTimestamp:      Tue, 02 Apr 2019 14:51:46 -0500
Labels:                 app=php-api
                        io.codefresh.account.name=eearleyotus
                        io.codefresh.auto-generated=fa9a935d-b399-4c62-8ff5-8becdfdff5ef
                        io.codefresh.generated-at=1554234706221
                        io.codefresh.pipeline.id=5c86862934520463544410b7
                        io.codefresh.pipeline.name=bitbucket-bitbucket-otusteam-source-code-source-code
                        io.codefresh.process.id=5caa15e635b49bdb152f77d8
                        io.codefresh.scm.branch=master
                        io.codefresh.scm.revision=0710490e71d29cf7ad2d1f2934b862c3a9ba715a
Annotations:            deployment.kubernetes.io/revision=32
                        kubectl.kubernetes.io/last-applied-configuration={"apiVersion":"extensions/v1beta1","kind":"Deployment","metadata":{"annotations":{"deployment.kubernetes.io/revision":"31"},"generation":34,"labels":{"...
Selector:               app=php-api,io.codefresh.auto-generated=fa9a935d-b399-4c62-8ff5-8becdfdff5ef,io.codefresh.generated-at=1554234706221
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  50% max unavailable, 50% max surge
Pod Template:
  Labels:       app=php-api
                io.codefresh.auto-generated=fa9a935d-b399-4c62-8ff5-8becdfdff5ef
                io.codefresh.generated-at=1554234706221
  Annotations:  forceRedeployUniqId=80b29683-f4db-4a99-8c62-48070092e82f
                forceRedeployUniqueId=1554652929471
  Containers:
   php-api:
    Image:        r.cfcr.io/eearleyotus/otus/php-api:master-0710490
    Port:         80/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
OldReplicaSets:  <none>
NewReplicaSet:   php-api-7794478f5 (1/1 replicas created)
Events:          <none>
```



