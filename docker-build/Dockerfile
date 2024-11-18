FROM amazonlinux:2023 as builder

ARG NODE_VERSION=20.18.0
ARG NVM_DIR=/usr/local/nvm

ARG PYTHON_VERSION=3.12.2
ARG PYENV_ROOT=/usr/local/pyenv

RUN yum groupinstall -y -q "Development Tools"
RUN yum install -y -q zlib-devel bzip2-devel readline-devel sqlite-devel openssl-devel tk-devel libffi-devel xz-devel

RUN curl https://pyenv.run | bash
RUN $PYENV_ROOT/bin/pyenv install $PYTHON_VERSION && $PYENV_ROOT/bin/pyenv global $PYTHON_VERSION

RUN mkdir -p $NVM_DIR
RUN curl https://raw.githubusercontent.com/creationix/nvm/v0.40.1/install.sh | bash
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION && nvm use $NODE_VERSION"

ENV NODE_PATH $NVM_DIR/versions/node/v$NODE_VERSION/lib/node_modules
ENV PATH $PYENV_ROOT/versions/$PYTHON_VERSION/bin:$NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

RUN mkdir -p /var/task
WORKDIR /var/task

ENTRYPOINT ["npm", "install"]
