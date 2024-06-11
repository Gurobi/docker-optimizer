#
# Docker file to create a Python Environment
#

FROM ubuntu:20.04 as buildoptimizer
ARG GRB_VERSION=11.0.0
ARG GRB_SHORT_VERSION=11.0
ARG TARGETPLATFORM

# Create a script to determine GRB_PLATFORM based on TARGETPLATFORM
RUN if [ "$TARGETPLATFORM" = "linux/arm64" ]; then \
        echo "armlinux64" > /platform.txt; \
      else \
        echo "linux64" > /platform.txt; \
    fi

ENV GRB_PLATFORM=${GRB_PLATFORM}

# install gurobi package and copy the files
WORKDIR /opt

RUN export GRB_PLATFORM=$(cat /platform.txt) && echo $GRB_PLATFORM \
    &&apt-get update \
    && apt-get install --no-install-recommends -y\
       ca-certificates  \
       wget \
    && update-ca-certificates \
    && wget -v https://packages.gurobi.com/${GRB_SHORT_VERSION}/gurobi${GRB_VERSION}_$GRB_PLATFORM.tar.gz \
    && tar -xvf gurobi${GRB_VERSION}_$GRB_PLATFORM.tar.gz  \
    && rm -f gurobi${GRB_VERSION}_$GRB_PLATFORM.tar.gz \
    && mv -f gurobi* gurobi \
    && rm -rf gurobi/$GRB_PLATFORM/docs \
    && mv -f gurobi/$GRB_PLATFORM*  gurobi/linux

# After the file renaming, a clean image is build
FROM python:3.10-slim-bullseye AS packageoptimizer

ARG GRB_VERSION=11.0.0

LABEL vendor="Gurobi"
LABEL version=${GRB_VERSION}

# update system and certificates
RUN apt-get update \
    && apt-get install --no-install-recommends -y\
       ca-certificates  \
       p7zip-full \
       zip \
    && update-ca-certificates \
    && python -m pip install gurobipy==${GRB_VERSION} \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /opt/gurobi
COPY --from=buildoptimizer /opt/gurobi .

ENV GUROBI_HOME /opt/gurobi/linux
ENV PATH $PATH:$GUROBI_HOME/bin
ENV LD_LIBRARY_PATH $GUROBI_HOME/lib

WORKDIR /opt/gurobi/linux


CMD ["gurobi.sh"]