FROM amazonlinux as builder
ARG NODE_VERSION=16.20.2
ARG NVM_DIR=/usr/local/nvm

RUN yum groupinstall -yq "Development Tools"

RUN mkdir -p $NVM_DIR
RUN curl https://raw.githubusercontent.com/creationix/nvm/v0.40.1/install.sh | bash
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION && nvm use $NODE_VERSION"

ENV NODE_PATH $NVM_DIR/versions/node/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

RUN mkdir -p /var/task
WORKDIR /var/task

ENTRYPOINT ["npm", "install"]
