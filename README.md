![Logo](https://cdn.gurobi.com/wp-content/uploads/GurobiLogo_Black.svg "Gurobi Optimization")
# Quick reference
Maintained by: [Gurobi Optimization](https://www.gurobi.com)

Where to get help: [Gurobi Support](https://www.gurobi.com/support/), [Gurobi Documentation](https://www.gurobi.com/documentation/)

# Supported tags and respective Dockerfile links

* [11.0.2, latest](https://github.com/Gurobi/docker-optimizer/blob/master/11.0.2/Dockerfile)
* [11.0.1](https://github.com/Gurobi/docker-optimizer/blob/master/11.0.1/Dockerfile)
* [11.0.0](https://github.com/Gurobi/docker-optimizer/blob/master/11.0.0/Dockerfile)
* [10.0.3](https://github.com/Gurobi/docker-optimizer/blob/master/10.0.3/Dockerfile)
* [10.0.2](https://github.com/Gurobi/docker-optimizer/blob/master/10.0.2/Dockerfile)
* [10.0.1](https://github.com/Gurobi/docker-optimizer/blob/master/10.0.1/Dockerfile)
* [10.0.0](https://github.com/Gurobi/docker-optimizer/blob/master/10.0.0/Dockerfile)
* [9.5.2](https://github.com/Gurobi/docker-optimizer/blob/master/9.5.2/Dockerfile)
* [9.5.1](https://github.com/Gurobi/docker-optimizer/blob/master/9.5.1/Dockerfile)
* [9.5.0](https://github.com/Gurobi/docker-optimizer/blob/master/9.5.0/Dockerfile)

When building a production application, we recommend using an explicit version number instead of the `latest` tag.
This way, you are in control of the upgrade process of your application.

# Quick reference (cont.)

Supported architectures: linux amd64

Published image artifact details: https://github.com/Gurobi/docker-optimizer

Gurobi images available on DockerHub:
- [gurobi/optimizer](https://hub.docker.com/r/gurobi/optimizer): Gurobi Optimizer (full distribution)
- [gurobi/python](https://hub.docker.com/r/gurobi/python): Gurobi Optimizer (Python API only)
- [gurobi/python-example](https://hub.docker.com/r/gurobi/python-example): Gurobi Optimizer example in Python with a WLS license
- [gurobi/modeling-examples](https://hub.docker.com/r/gurobi/modeling-examples): Optimization modeling examples (distributed as Jupyter Notebooks)
- [gurobi/compute](https://hub.docker.com/r/gurobi/compute): Gurobi Compute Server
- [gurobi/manager](https://hub.docker.com/r/gurobi/manager): Gurobi Cluster Manager

# What is `gurobi/optimizer`?
The Gurobi Optimizer is the fastest and most powerful mathematical programming solver available 
for your LP, QP and MIP (MILP, MIQP, and MIQCP) problems.
More info at the [Gurobi Website](https://www.gurobi.com/products/gurobi-optimizer/).

The Gurobi Optimizer supports of a wide range of programming and modeling languages, see 
the [reference manual](https://www.gurobi.com/documentation/current/refman/index.html).

The `gurobi/optimizer` image provides a base Docker image for building applications using any of
the supported APIs (C, C++, Java, .NET, Python, MATLAB, and R), as well as the command line tools
such as `gurobi_cl` and the Python shell. If you are planning to only use the Python API, 
we recommend using the `gurobi/python` [image](https://hub.docker.com/r/gurobi/python) instead.

## Getting a Gurobi license

The Gurobi Optimizer requires a license.  To run it in a Docker container, you have
a few options:

* The [Web License Service](https://www.gurobi.com/web-license-service/) (WLS) is a new Gurobi licensing service 
  for containerized environments (Docker, Kubernetes...). Gurobi components can automatically request and renew license tokens to 
  the WLS servers available in several regions worldwide. WLS only requires that your container has access to the 
  Internet. Commercial users can request an evaluation and academic users can request a free license.
  Please register to access the [Web License Manager](https://license.gurobi.com) and read the
  [documentation](https://license.gurobi.com/manager/doc/overview)

* A [Gurobi Compute Server](https://www.gurobi.com/products/gurobi-compute-server/) 
allows you to seamlessly offload your optimization computations onto one or more dedicated 
optimization servers grouped in a cluster. Users and applications can share the servers 
thanks to advanced queuing and load balancing capabilities. Users can monitor jobs, and 
administrators can manage the servers. The cluster manager provides additional features
and security management. The Compute Server, and the Cluster Manager can 
be installed outside of the containerized environment using a standard license, or within the 
containerized environment with a WLS license.

* The [Gurobi Cloud](https://www.gurobi.com/products/gurobi-instant-cloud/) is a simple and 
cost-effective way to get up and running with powerful Gurobi optimization software running 
on cloud services. It allows you to launch one or more computers, pre-loaded with Gurobi 
software and dedicated to you on Microsoft Azure® and Amazon Web Services®. 

* A [Gurobi Token Server](https://www.gurobi.com/documentation/current/quickstart_linux/creating_a_token_server_cl.html) 
runs on a dedicated machine outside of the Docker cluster. Client programs running in
Docker containers can request tokens from the token server.

Note that other standard license types (NODE, Academic) do not work with containers.
Please contact your sales representative at [sales@gurobi.com](mailto:sales@gurobi.com) to discuss licensing options. 

## Using the client license

You will need to specify a set of properties to 
connect to a Compute Server cluster, the Gurobi Cloud, or a token server. To do so,
you have the following options:
* Mounting the client license file:
A client license file (usually called `gurobi.lic`) contains connection 
parameters. It can be mounted to the container. 
This option provides a simple approach for testing with Docker.
When using Kubernetes, the license file can be stored as a secret and mounted in the container.

* Setting parameters with the API:
When your application creates a [Gurobi environment](https://www.gurobi.com/documentation/current/refman/index.html), 
you can specify connection parameters through the API. The parameter values can come from 
environment variables, a database or from other sources as required by your application. 

A quick guide to the appropriate API parameters and license file properties is available [here](https://github.com/Gurobi/docker-optimizer/blob/master/PARAMS.md).

We do not recommend adding the license file to the Docker image itself. It is not a flexible 
solution as you may not reuse the same image with different settings. More importantly, it is not secure
as some license files need to contain credentials in the form of API keys that should remain private.

## Testing with model examples 
In the following command-line examples, we will run model files stored on 
your local machines. The model files must be stored in a local directory that
will be mounted to the instance.

In the current directory (retrieved using `$PWD`), create a sub-directory with the 
models you would like to run:
 
    Directory: `$PWD/models`
    Content: `poolsearch.py`, `stein9.mps`
    
See some [model examples](https://github.com/Gurobi/docker-optimizer/tree/master/models).
    
    
# How to use this image?

## Building a custom image

This image can be used directly for some tests, but the main goal is to help build applications using 
the Gurobi API. This image can be used as a base image, and specific application dependencies 
can be added. Here is an example of a `Dokerfile`:

File `Dockerfile`
```
# Indicate the Gurobi reference image
FROM gurobi/optimizer:latest

# Set the application directory
WORKDIR /app

# Copy the application code 
ADD . /app

# Command used to start the application
CMD [...]
```

Once the custom image is built, it can be deployed using Docker, Docker Compose
or Kubernetes.
```
docker build -t my-gurobi-app .
```

As already mentioned, the license file should not be copied into the image, and we will 
give example about how to mount the license file in the next sections.


## Using Docker

### Start a `gurobi/optimizer` shell instance
```console
$ docker run --volume=$PWD/gurobi.lic:/opt/gurobi/gurobi.lic:ro  \
             --volume=$PWD/models:/models \
             -it gurobi/optimizer
```

... where `$PWD` is the current directory.

Then run in the console:
```console
gurobi> m = read('/models/stein9.mps')

gurobi> m.optimize()

```

### Optimizing with a `gurobi/optimizer` instance

The following command line starts the `gurobi/optimizer` container, mounts a directory
that contains a few local models, and then it optimizes the model `stein9.mps`:

```console
$ docker run --volume=$PWD/gurobi.lic:/opt/gurobi/gurobi.lic:ro \
             --volume=$PWD/models:/models:ro \
             gurobi/optimizer gurobi_cl /models/stein9.mps
```

If you need to enable client/server logging, you can set the `GRB_CLIENT_LOG` variable:

```console
$ docker run --env=GRB_CLIENT_LOG=3 \
             --volume=$PWD/gurobi.lic:/opt/gurobi/gurobi.lic:ro \
             --volume=$PWD/models:/models:ro  \
             gurobi/optimizer /models/poolsearch.py
```

### Optimizing with a custom application

If you have built a custom image, you can apply the same concepts:
```console
$ docker run --env=GRB_CLIENT_LOG=3  \
             --volume=$PWD/gurobi.lic:/opt/gurobi/gurobi.lic:ro \
             my-gurobi-app
```

## Using Docker Compose

Docker Compose can be used if your application requires different components (database, 
frontend WebUI, backend services...). Docker Compose will help build and connect these 
components.  For a local test, you can mount the license file as a volume.

Example `docker-compose.yml` for a Gurobi python instance:

```
version: '3.7'
services:
  gurobi:
    image: <your-own-custom-image>
    volumes:
      - ./gurobi.lic:/opt/gurobi/gurobi.lic:ro

```

Run `$ docker-compose up --build ` to build and run you application.

## Using Kubernetes

In a similar way, Kubernetes can be used to deploy your application in a cluster. 
Here is an example of a deployment descriptor `deployment.yaml` for an application using 
the custom image `<your-own-custom-image>`:

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: optim
  labels:
    name: optim
spec:
  selector:
    matchLabels:
      name: optim
  replicas: 1
  template:
    metadata:
      labels:
        name: optim
    spec:
      volumes:
        - name: gurobi-lic
          secret:
            secretName: gurobi-lic
      containers:
        - name: optim
          image: <your-own-custom-image>
          imagePullPolicy: IfNotPresent
      volumeMounts:
        - name: gurobi-lic
          mountPath: "/opt/gurobi_lic"
          readOnly: true
      env:
        - name: GRB_LICENSE_FILE
          value: "/opt/gurobi_lic/gurobi.lic"
```

Before deploying your application, we recommend storing the license file as a secret and
mounting it inside the container.
```
kubectl create secret generic gurobi-lic --from-file="gurobi.lic=$PWD/gurobi.lic"
kubectl apply -f deployment.yaml
```

If you are deploying your custom image and using the [Cluster Manager](https://hub.docker.com/r/gurobi/manager) 
within the same cluster, you will need to connect your application to the Cluster Manager.
To do so, we recommend the following:
- Create a system user in the Cluster Manager and generate an API key.
- Declare the API key as a secret.
```
kubectl create secret generic gurobi-manager --from-literal=accessId=xxxxx --from-literal=secret=xxxxxx
```
- Use environment variables to pass the API key and the manager URL.
```
          env:
            - name: GRB_CSMANAGER
              value: "http://$(GUROBI_MANAGER_SERVICE_HOST):$(GUROBI_MANAGER_SERVICE_PORT)"
            - name: GRB_CSAPIACCESSID
              valueFrom:
                secretKeyRef:
                  name: gurobi-manager
                  key: accessId
            - name: GRB_CSAPISECRET
              valueFrom:
                secretKeyRef:
                  name: gurobi-manager
                  key: secret
```
- Finally, in your application, assign the Gurobi environment parameters from the variables, here is an 
example with Python:
```
        env = Env(empty=True)
        csManager = os.getenv('GRB_CSMANAGER','')
        if csManager:
            env.setParam('CSManager', csManager)

        csAPIAccessId = os.getenv('GRB_CSAPIACCESSID','')
        if csAPIAccessId:
            env.setParam('CSAPIAccessID', csAPIAccessId)

        csAPISecret = os.getenv('GRB_CSAPISECRET','')
        if csAPISecret:
            env.setParam('CSAPISecret', csAPISecret)

        env.start()
```

## Environment Variables

The following environment variables can be used:

* `GRB_CLIENT_LOG`: Turns Client Server logging on or off. Options are off (0), only error messages (1), information and error messages (2), or (3) verbose, information, and error messages.

# License

By downloading and using this image, you agree with the 
[End-User License Agreement](https://www.gurobi.com/EULA) for the Gurobi software contained in this image.

As with all Docker images, these likely also contain other software which may be under other
licenses (such as Bash, etc from the base distribution, along with any direct or indirect
dependencies of the primary software being contained).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use
of this image complies with any relevant licenses for all software contained within.
