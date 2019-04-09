# Hostnames

### Hosts names:

1. [qb.platform-int.otus.com](qb.platform-int.otus.com.md)
2. [napi.platform-int.otus.com](napi.platform-int.otus.com.md)
3. [papi.platform-int.otus.com](papi.platform-int.otus.com.md)
4. [stage-fe.platform-int.otus.com](stage-fe.platform-int.otus.com.md)

### How I can discover all the hostnames?

Using the "kubectl" you'll be able to discover all the hosts configured to the Otus' application.

```bash
$ kubectl get ingress echo-ingree -o yaml 
```

You can find it under the property spec:

```text
spec:
...
  tls:
    - hosts:
      - echo1.platform-int.otus.com
      - echo2.platform-int.otus.com
      - qb.platform-int.otus.com
      - napi.platform-int.otus.com
      - papi.platform-int.otus.com
      - stage-fe.platform-int.otus.com
      secretName: letsencrypt-prod
```

with 'jq' cli you can filter all the hosts:

```text
$ kubectl get ingress echo-ingress -o json | jq '.spec.rules[].host'
```

It should return a list like this:

```text
"echo1.platform-int.otus.com"
"echo2.platform-int.otus.com"
"qb.platform-int.otus.com"
"napi.platform-int.otus.com"
"papi.platform-int.otus.com"
"stage-fe.platform-int.otus.com"
```

### How I find the serviceName?

The "ingress" namespace works as a load balancer, because of that it contains the configuration of all the hostnames and its respective service name.   
The command below tries to simplify the view to see just the hostnames and its respective service name. 

```text
$ kubectl get ingress echo-ingress -o json | jq '.spec.rules | map((.host + " ==> " + (.http.paths | map(.backend.serviceName) | join(","))))'
```

It'll return the data formatted like "hostname ==&gt; serviceName":

```text
[
  "echo1.platform-int.otus.com ==> echo1",
  "echo2.platform-int.otus.com ==> echo2",
  "qb.platform-int.otus.com ==> alexander",
  "napi.platform-int.otus.com ==> node-api",
  "papi.platform-int.otus.com ==> php-api",
  "stage-fe.platform-int.otus.com ==> ci-staging-fe"
]
```

### How can I learn more about the service?

To learn more about one of the hostname, you can get the "serviceName" and run the following command:

```text
$ kubectl describe service YOUR_SERVICE_NAME
```

Although, for you know more about how many pods this service required you need to access the deployment information about this service.

```text
$ kubectl describe deployment YOUR_SERVICE_NAME
```

### How are the environments released?

For the environments' release is used the Codefresh.com platform for CI/CD.  
There're 3 types of environment:

* **Production** The environment used for the clients. 
* **Staging** The environment used for a Quality test. This environment will reflect what will be deployed on the next release. 
* **Web-dev** This environment is used to test major features that are still in development.

{% hint style="info" %}
Each environment will be a namespace in the kubernets environment.
{% endhint %}

Each time that a commit is made, CodeFresh will run a step by step define in the service pipeline.  
In general, all the hostnames' environment is configured to run:

1. Cloning main repository
2. Sonar \(Code Quality tool\)
3. Compile/Test Unit
4. Build
5. Deploy

The code will be deployed to :

* **Staging** if the branch is merged to the **candidate** branch.
* **Web-Dev** if the branch is merged to the **develop** branch.
* **Production** if the branch is merged to **master**.

### How frequent are they released?

The production environment is released every 2 weeks.  
The staging and web-dev are released through the sprint.

Others environments that will provide some functionality for the entire application, like:

* MySQL
* Redis
* Elastic Search
* Load Balancer

Will just be deployed when some configuration needs to be changed.

