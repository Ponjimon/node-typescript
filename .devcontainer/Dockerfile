# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.233.0/containers/typescript-node/.devcontainer/base.Dockerfile

# [Choice] Node.js version (use -bullseye variants on local arm64/Apple Silicon): 18, 16, 14, 18-bullseye, 16-bullseye, 14-bullseye, 18-buster, 16-buster, 14-buster
ARG NODE_VERSION="20"
ARG UBUNTU_VERSION="bullseye"
ARG PNPM_VERSION="8"
FROM mcr.microsoft.com/vscode/devcontainers/typescript-node:0-${NODE_VERSION}-${UBUNTU_VERSION}
# Need to redeclare this build arg so it's available after FROM again
ARG UBUNTU_VERSION="bullseye"

RUN npm install -g pnpm@${PNPM_VERSION}

# Add Cloudflare Repository
RUN mkdir -p --mode=0755 /usr/share/keyrings
RUN curl -fsSL https://pkg.cloudflare.com/cloudflare-main.gpg | tee /usr/share/keyrings/cloudflare-main.gpg >/dev/null
RUN echo 'deb [signed-by=/usr/share/keyrings/cloudflare-main.gpg] https://pkg.cloudflare.com/cloudflared' "${UBUNTU_VERSION}" 'main' | tee /etc/apt/sources.list.d/cloudflared.list
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive && apt-get install -y --no-install-recommends cloudflared
