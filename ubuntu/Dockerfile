ARG UBUNTU_VERSION

FROM ubuntu:${UBUNTU_VERSION} AS builder

# Terraform versions : https://releases.hashicorp.com/terraform/
ARG TERRAFORM_VERSION
ENV TERRAFORM_VERSION=${TERRAFORM_VERSION}
LABEL terraform_version=${TERRAFORM_VERSION}

RUN apt update \
    && apt install -y curl unzip \
    && curl -LO https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
    && unzip '*.zip' -d /usr/local/bin

FROM ubuntu:${UBUNTU_VERSION}

COPY --from=builder /usr/local/bin/terraform /usr/local/bin

RUN apt update \
    && apt install -y ca-certificates \
    && rm -rf /var/lib/apt/lists/* /var/cache/* \
    && useradd --system terraform

USER terraform
WORKDIR /home/terraform

ENTRYPOINT ["/usr/local/bin/terraform"]