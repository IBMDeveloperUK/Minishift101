# Lab 3: Managing your OpenShift applications

You have learnt how to create an OpenShift application but how do you then manage it once it has been created? 

## 1. Checking the build status

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
