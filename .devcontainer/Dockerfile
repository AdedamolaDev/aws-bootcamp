FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

# Install system utilities
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends curl unzip wget gnupg software-properties-common tree \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install Node.js LTS (required for AWS CDK) - always gets latest LTS at build time
RUN curl -fsSL https://deb.nodesource.com/setup_lts.x | bash - \
    && apt-get install -y nodejs \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install AWS CLI - always downloads latest version from AWS
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && ./aws/install \
    && rm -rf awscliv2.zip aws

# Install AWS CDK - always installs latest version from npm
RUN npm install -g aws-cdk@latest

# Install Terraform - always installs latest version from HashiCorp repo
RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg \
    && echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list \
    && apt-get update \
    && apt-get install -y terraform \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install PowerShell - always installs latest version from Microsoft repo
RUN wget -q https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb \
    && dpkg -i packages-microsoft-prod.deb \
    && rm packages-microsoft-prod.deb \
    && apt-get update \
    && apt-get install -y powershell \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*
