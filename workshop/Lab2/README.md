# Lab 2: Creating OpenShift applications

After creating a project as instructed in the [previous lab (Lab 1)](../Lab1/README.md), the next step is to create an OpenShift application in the cluster.

## 1. Creating an app 

There are several ways in which you can create an app in OpenShift:

- From source code
- From DockerHub images
- From OpenShift templates
- From the OpenShift UI

### 1.1 Creating an app from source

With `oc new-app` command, you can create an application in OpenShift from some existing source code either locally or with the url to the repository. If a source repository is specified, `new-app` will either check to see which build strategy to use (**Docker** or **Source**). 

With the former, a runnable image is created, whereas as the latter will try to identify the language by looking at the files in the project's root directory and then use an appropriate builder. 

To build from a local Dockerfile:
```
$ oc new-app /path/to/local/or/remote/Dockerfile
```

To build from source:
```
$ oc new-app path/to/local/or/remote/repository.git
```

### 1.2 Creating an app from a DockerHub image

Similar to Docker, OpenShift is also configured to the public image registry DockerHub. If you specify an image that exists in DockerHub, the `new-app` command will create a runnable image directly from this image. 

For example, if you wanted to create an app from the official nginx image, you would run:
```
$ oc new-app nginx
```

You not only limited to the DockerHub registry but as with Docker, you are able to specify images that are stored in private registries too:
```
$ oc new-app myregistry:8000/example/image
```

### 1.3 Creating an app from an OpenShift template

OpenShift templates are basically starter applications that have been configured ready for OpenShift. These cover frequently used applications deployed in containers e.g. Ruby, Node and MongoDB. 

The [ruby template](https://github.com/sclorg/nodejs-ex#openshift-origin-v3-setup) looks as follows:

```
nodejs-ex
├── openshift
│   └── templates
│       ├── nodejs.json
│       ├── nodejs-mongodb.json
│       └── nodejs-mongodb-persistent.json
├── package.json
├── README.md
├── server.js
├── tests
│   └── app_test.js
└── views
    └── index.html
```

To deploy it, you can run:

```
$ oc new-app -f /path/to/nodejs.json
```

As this template lives in a repo, we could have also run this from source as described in [section 1.1](./#11-creating-an-app-from-source)

### 1.4 Creating an app from the OpenShift UI

If you're not a fan of the cli and wanted a more visual way of deploying applications in your cluster, you also have the option of the OpenShift console. This is available locally at the address given after running `minishift start` as we did in the [setup](https://github.com/mofesal/minishift-101/blob/master/workshop/README.md#start-the-openshift-server):

```console
$ minishift start
...

The server is accessible via web console at:
    https://192.168.64.11:8443/console

You are logged in as:
    User:     developer
    Password: <any value>
```

Login to the UI:

![OpenShift login](../images/openshift_login.png)

As mentioned in the `minishift start` output, you can use the user _developer_ and password as any string of characters (at least one) and you will be able to access the UI.

Access the catalog:

![OpenShift catalog](../images/openshift_console.png)

Once you login, you will be redirected to the browser catalog where there will be a number of sample applications available for you to chose to deploy. This mirrors the OpenShift template steps we saw in [section 1.2](./#12-creating-an-app-from-a-dockerhub-image). We can also create and switch between projects but note, you are limited to the provided sample applications available in the UI.

See this [reference](https://docs.openshift.com/enterprise/3.0/dev_guide/new_app.html) for a more comprehensive overview of how to use the `new-app` command to create OpenShift applications.

Congratulations! You have learnt several ways to create applications in OpenShift! To see how we can manage our applications in OpenShift, let's continue on to the [next Lab (Lab 3)](../Lab3/README.md)
