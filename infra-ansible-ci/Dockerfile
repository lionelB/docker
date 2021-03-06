FROM python:2.7

# install dependencies (gettext-base to install envsubst)
RUN apt-get update \
    && apt-get -y install gettext-base=0.19.8.1-9 jq=1.5+dfsg-2+b1 curl=7.64.0-4 apt-transport-https=1.8.2 \
      lsb-release=10.2019051400 gnupg=2.2.12-1+deb10u1 --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# install terraform
RUN curl https://releases.hashicorp.com/terraform/0.11.14/terraform_0.11.14_linux_386.zip -o terraform.zip \
    && unzip terraform.zip \
    && mv terraform /usr/bin/ \
    && terraform --version

# install ansible & linter
RUN pip install 'ansible[azure]'==2.8.1 ansible-lint==4.1.0 yamllint==1.16.0 yq==2.9.2

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

# install azure CLI
RUN curl -sL https://packages.microsoft.com/keys/microsoft.asc | \
        gpg --dearmor | \
        tee /etc/apt/trusted.gpg.d/microsoft.asc.gpg > /dev/null \
    && echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ stretch main" | tee /etc/apt/sources.list.d/azure-cli.list \
    && apt-get update && apt-get install -y azure-cli=2.0.76-1~stretch --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
