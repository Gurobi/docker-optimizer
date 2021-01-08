![Logo](https://www.gurobi.com/wp-content/uploads/2018/12/logo-final.png "Gurobi Optimization")
# Quick reference
Maintained by: [Gurobi Optimization](https://www.gurobi.com)

Where to get help: [Gurobi Support](https://www.gurobi.com/support/), [Gurobi Documentation](https://www.gurobi.com/documentation/)

# Supported tags and respective Dockerfile links
## Simple Tags
* [9.1.1, latest](https://github.com/Gurobi/docker-optimizer/blob/master/9.1.1/Dockerfile)

# Quick reference (cont.)

Supported architectures: linux amd64

Published image artifact details: https://github.com/Gurobi/docker-optimizer

Gurobi images available on DockerHub:
- [gurobi/optimizer](https://hub.docker.com/repository/docker/gurobi/optimizer): Gurobi Optimizer (full distribution)
- [gurobi/python](https://hub.docker.com/repository/docker/gurobi/python): Gurobi Optimizer (Python API only)
- [gurobi/modeling-examples](https://hub.docker.com/repository/docker/gurobi/modeling-examples): Optimization modeling examples (distributed as Jupyter Notebooks)
- [gurobi/compute](https://hub.docker.com/repository/docker/gurobi/compute): Gurobi Compute Server
- [gurobi/manager](https://hub.docker.com/repository/docker/gurobi/manager): Gurobi Cluster Manager

# What is `gurobi/optimizer`?
The Gurobi Optimizer is the fastest and most powerful mathematical programming solver available 
for your LP, QP and MIP (MILP, MIQP, and MIQCP) problems.
More info at the [Gurobi Website](https://www.gurobi.com/products/gurobi-optimizer/).

The Gurobi Optimizer supports of a wide range of programming and modeling languages, see 
the [reference manual](https://www.gurobi.com/documentation/current/refman/index.html).

The `gurobi/optimizer` image provides a base Docker image for building applications using any of
the supported APIs (C, C++, Java, .NET, Python, MATLAB, and R), as well as the command line tools
such as `gurobi_cl` and the Python shell. If you are planning to only use the Python API, 
we recommend using the `gurobi/python` [image](https://hub.docker.com/repository/docker/gurobi/python) instead.

## Getting a Gurobi license

The Gurobi Optimizer requires a license.  To run it in a Docker container, you have
a few options:

* A [Gurobi Compute Server](https://www.gurobi.com/products/gurobi-compute-server/) 
allows you to seamlessly offload your optimization computations onto one or more dedicated 
optimization servers grouped in a cluster. Users and applications can share the servers 
thanks to advanced queuing and load balancing capabilities. Users can monitor jobs, and 
administrators can manage the servers. The cluster manager provides additional features
and security management. The Compute Server, and the Cluster Manager must 
be installed outside of the Docker cluster.

* The [Gurobi Cloud](https://www.gurobi.com/products/gurobi-instant-cloud/) is a simple and 
cost-effective way to get up and running with powerful Gurobi optimization software running 
on cloud services. It allows you to launch one or more computers, pre-loaded with Gurobi 
software and dedicated to you on Microsoft Azure® and Amazon Web Services®. 

* A [Gurobi Token Server](https://www.gurobi.com/documentation/current/quickstart_linux/creating_a_token_server_cl.html) 
runs on a dedicated machine outside of the Docker cluster. Client programs running in
Docker containers can request tokens from the token server.

* Please contact your sales representative at [sales@gurobi.com](mailto:sales@gurobi.com) to discuss additional options. 

Note that other standard license types (NODE, Academic) do not work with Docker.

## Using the client license

You will need to specify a set of properties to 
connect to a Compute Server cluster, the Gurobi Cloud, or a token server. To do so,
you have the following options:
* Mounting the client license file:
A client license file (usually called `gurobi.lic`) contains connection 
parameters. It can be mounted to the container. This option provides a simple approach for testing.

* Setting parameters with the API:
When your application creates a [Gurobi environment](https://www.gurobi.com/documentation/current/refman/index.html), 
you can specify connection parameters through the API. The parameter values can come from 
environment variables, a database or from other sources as required by your application. 
This is the recommended approach for production applications.

A quick guide to the appropriate API parameters and license file properties is available [here](https://github.com/Gurobi/docker-optimizer/blob/master/PARAMS.md).

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

## Start a `gurobi/optimizer` shell instance
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

## Optimizing with a `gurobi/optimizer` instance

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

## ... via docker stack deploy or docker-compose
Example `docker-compose.yml` for a Gurobi python instance:

```
version: '3.7'
services:
  optimizer:
    image: gurobi/python:latest
    volumes:
      - ./models:/models:ro
      - ./gurobi.lic:/opt/gurobi/gurobi.lic:ro

```

Run `$ docker-compose run optimizer /models/poolsearch.py `

## How to use this image as a base image?
This image can also be used as a base image for applications using Gurobi.


File `Dockerfile`
```
FROM gurobi/optimizer:latest
...

RUN ...

...

```

## Environment Variables

The following environment variables can be used:

* `GRB_CLIENT_LOG`: Turns Client Server logging on or off. Options are off (0), only error messages (1), information and error messages (2), or (3) verbose, information, and error messages.

# License

View the [End User License Agreement](https://www.gurobi.com/wp-content/uploads/2020/11/EULA_standard.pdf) for the software contained in this image.

As with all Docker images, these likely also contain other software which may be under other
licenses (such as Bash, etc from the base distribution, along with any direct or indirect
dependencies of the primary software being contained).

As for any pre-built image usage, it is the image user's responsibility to ensure that any use
of this image complies with any relevant licenses for all software contained within.
