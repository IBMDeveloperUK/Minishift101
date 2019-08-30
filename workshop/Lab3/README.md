# Lab 3: Managing your OpenShift applications

You have learnt how to create an OpenShift application but how do you then manage it once it has been created? 

## 1. Monitoring builds

When we run `oc new-app` a build is triggered similar to a `docker build`. Unlike `docker build` however, the build happens in the background and we don't get the output of what is happening. 

To see this output, we can run:

```console
$ oc status
```

Assuming we were building the ruby template we would run:

```
$ oc new-app https://github.com/sclorg/nodejs-ex
```

Then to check the status:

```console
$ oc status
In project nodejs (nodejs-echo) on server https://192.168.64.11:8443

svc/nodejs-ex - 172.30.6.48:8080
  dc/nodejs-ex deploys istag/nodejs-ex:latest <-
    bc/nodejs-ex source builds https://github.com/sclorg/nodejs-ex on openshift/nodejs:10
      build #1 running for 36 hours
    deployment #1 waiting on image or update


2 infos identified, use 'oc status --suggest' to see details.
```

Looking at the output, we can see that we have a service endpoint to access our node app at `172.30.6.48:8080`. We can also see the build type used to create our application: `openshift/nodejs:10`. Finally, we can see in the last line that our application is not actually ready for usage as it is waiting for thr image to be deployed. In the line above, we can use the build number to get a more comprehensive idea of what is happening in the build.

If you wanted to check the build progress of a application, it would follow this format:
```
$ oc logs build/<app-name>-<build-no>
```

In this example, we would use the application name `nodejs-ex` and the build number `1`:
```
$ oc logs build/nodejs-ex-1
```

## 2. Monitoring deployments

In Kubernetes, we are able to the status of all our running applications. OpenShift has the same capability using the `oc` command:

```console
$ oc get pod
NAME                READY     STATUS      RESTARTS   AGE
nodejs-ex-1-build   0/1       Completed   0          13m
nodejs-ex-1-hx6v9   1/1       Running     0          12m
```

Here we can see that a pod (`nodejs-ex-1-build`) was created with the sole purpose to run the build and then was cleaned up after completing successfully. We are then left with our running pod (`nodejs-ex-1-hx6v9`) containing our node application.

If we actually just wanted to see the _deployments_, the actual application and not the assoicated pods, we can run:

```console
$ oc get dc
NAME        REVISION   DESIRED   CURRENT   TRIGGERED BY
nodejs-ex   1          1         1         config,image(nodejs-ex:latest)
```

Another useful command in Kubernetes is the ability to check the services associated with our applications if any. We do this in Kubernetes by running `kubectl get svc` and can do a similar thing in OpenShift:

```console
$ oc get svc
NAME        TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)    AGE
nodejs-ex   ClusterIP   172.30.6.48   <none>        8080/TCP   14m
```

As with Kubernetes, each application can be given an internal IP in which we can access our services but unless stated otherwise, this will only be available within the cluster.

Congratulations! You have learnt how to monitor your application builds and deployments within your cluster! To see how we can expose our applications outside of the OpenShift cluster, let's continue on to the [next Lab (Lab 4)](../Lab4/README.md)
