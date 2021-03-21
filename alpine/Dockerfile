ARG ALPINE_VERSION

FROM alpine:${ALPINE_VERSION}

# Ansible versions : https://releases.hashicorp.com/terraform/
ARG TERRAFORM_VERSION
ENV TERRAFORM_VERSION=${TERRAFORM_VERSION}
LABEL terraform_version=${TERRAFORM_VERSION}

RUN apk update && apk upgrade \
    && apk add --no-cache --virtual .build-deps --update curl unzip \
    && apk add --no-cache --update git \
    && curl -LO https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
    && unzip '*.zip' -d /usr/local/bin \
    && apk del .build-deps \
    && rm -rf /var/cache/apk/* /tmp/* /root/.cache .build-deps *.zip\
    && adduser -S terraform

USER terraform
WORKDIR /home/terraform

ENTRYPOINT ["/usr/local/bin/terraform"]