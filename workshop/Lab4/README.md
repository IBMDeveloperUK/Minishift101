## 4. Accessing our application

Once you have verified that your application is up and running, you may want to make sure that you can access your application outside of the cluster. There are several ways to do this:

- Node-port services
- Port-forwarding
- Routes

### 4.1 Node port services

This is the cleanest way to access the applications outside of OpenShift environment both locally and publicly. This way essentially makes use of the cluster node's IPs and a port in between the range (30000-32767) and tells OpenShift to proxy to the underlying application via. the port. This is better than the next two solutions for several reasons: we don't have to worry about port clashes, this works for non HTTP based services and finally, does not require a public host name. 

To expose our deployment via NodePort, we simply expose the deployment with a _load balancer_ type and label it with name _nodejs-ex-ingress_:
```console
$ oc expose dc nodejs-ex --type=LoadBalancer --name=nodejs-ex-ingress
service/nodejs-ex-ingress exposed
```

To see the NodePort created, we can run:
```console
$ oc get --export svc nodejs-ex-ingress
NAME                TYPE           CLUSTER-IP   EXTERNAL-IP    PORT(S)          AGE
nodejs-ex-ingress   LoadBalancer   <none>       172.29.51.89   8080:31692/TCP   <unknown>
```

We can use the NodePort in conjuction with the cluster's internal or external IP which we can find in the following command:
```console
$ oc get node -o wide
NAME        STATUS    ROLES     AGE       VERSION           INTERNAL-IP     EXTERNAL-IP   OS-IMAGE                KERNEL-VERSION              CONTAINER-RUNTIME
localhost   Ready     <none>    13h       v1.11.0+d4cacc0   192.168.64.11   <none>        CentOS Linux 7 (Core)   3.10.0-957.5.1.el7.x86_64   docker://1.13.1
```

We should then be able to access the application in the browser. In this example, we can access the Node application at `192.168.64.11:31692`:

![OpenShift node app](../images/openshift_node_app.png)

### 4.2 Port-forwarding

Alternatively, if you want to quickly access a port of a specific pod of your cluster, you can also use the oc `port-forward` command:

```
$ oc port-forward POD [LOCAL_PORT:]REMOTE_PORT
```

### 4.3 Routes

For web applications, the most common way to expose it is by a route. A route exposes the service as a host name. You can do this by running the command providing you have a host name available:

```
$ oc expose svc/nodejs-ex --hostname=www.example.com
```

Congratulations! You have completed all labs in this workshop! You have learnt how to:
- Create an OpenShift project
- Create an OpenShift application in various ways
- How to monitor the status of an application
- How to access and expose your application

For more information on how to navigate Minishift, check the [Minishift docs](https://docs.okd.io/latest/minishift/index.html)
