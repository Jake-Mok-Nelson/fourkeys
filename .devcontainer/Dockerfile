# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.241.1/containers/alpine/.devcontainer/base.Dockerfile

# [Choice] Alpine version: 3.15, 3.14, 3.13
ARG VARIANT="3.15"
FROM mcr.microsoft.com/vscode/devcontainers/base:0-alpine-${VARIANT}

# Install dependencies - docker, python/pip
ENV PYTHONUNBUFFERED=1
RUN apk add --update --no-cache docker python3 && \
    ln -sf python3 /usr/bin/python && \
    python3 -m ensurepip && \
    pip3 install --no-cache --upgrade pip setuptools

# Install Gcloud
RUN curl https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz > /tmp/google-cloud-sdk.tar.gz && \
    mkdir -p /usr/local/gcloud && \
    tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz && \
    rm /tmp/google-cloud-sdk.tar.gz && \
    /usr/local/gcloud/google-cloud-sdk/install.sh

# Adding the Gcloud path to local
ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin

# Get TFEnv (Terraform version manager)
RUN git clone --depth=1 https://github.com/tfutils/tfenv.git /home/vscode/.tfenv && \
    sudo chown -R vscode:vscode /home/vscode/.tfenv
COPY terraform-version /home/vscode/.tfenv/version
ENV PATH $PATH:/home/vscode/.tfenv/bin
