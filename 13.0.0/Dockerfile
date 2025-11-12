#
# Docker file to create a Python Environment


FROM ubuntu:24.04 as buildoptimizer
ARG GRB_VERSION=13.0.0
ARG GRB_SHORT_VERSION=13.0
ARG TARGETPLATFORM


RUN apt-get update \
    && apt-get install --no-install-recommends -y \
       ca-certificates \
       wget \
    && update-ca-certificates

WORKDIR /opt

RUN if [ "$TARGETPLATFORM" = "linux/arm64" ]; then \
        export GRB_PLATFORM="armlinux64"; \
      else \
        export GRB_PLATFORM="linux64"; \
    fi \
    && wget -v https://packages.gurobi.com/${GRB_SHORT_VERSION}/gurobi${GRB_VERSION}_$GRB_PLATFORM.tar.gz \
    && tar -xvf gurobi${GRB_VERSION}_$GRB_PLATFORM.tar.gz  \
    && rm *.tar.gz \
    && mv -f gurobi* gurobi \
    && mv -f gurobi/$GRB_PLATFORM*  gurobi/linux

# After the file renaming, a clean image is build
FROM python:3.10-slim-bookworm AS packageoptimizer

ARG GRB_VERSION=13.0.0

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

CMD ["gurobi_cl"]