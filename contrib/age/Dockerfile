# Set the PostgreSQL version
ARG PG_VERSION=15
FROM quay.io/coredb/c-builder:pg${PG_VERSION}
USER root
ARG PG_VERSION=15

# Extension build dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    libreadline-dev \
    zlib1g-dev \
    flex \
    bison \
    libxml2-dev \
    libxslt-dev \
    libssl-dev \
    libxml2-utils \
    xsltproc \
    ccache \
    python3 \
    python3-dev \
    python3-setuptools \
    python3-pip && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Clone repository
RUN git clone https://github.com/postgres/postgres.git

# Use argument to specify PostgreSQL release
ARG PG_RELEASE=REL_15_3

# Configure and build PostgreSQL
RUN cd postgres && \
    git fetch origin ${PG_RELEASE} && \
    git checkout ${PG_RELEASE} && \
    ./configure && \
    cd contrib && \
    git clone https://github.com/apache/age.git

RUN cd postgres/contrib/age && \
    git checkout release/PG${PG_VERSION}/1.5.0 && \
    make

