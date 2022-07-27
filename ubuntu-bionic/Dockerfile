FROM ubuntu:bionic

ARG DEBIAN_FRONTEND=noninteractive
ARG ENV_FILE="/root/.bashrc"

ENV HOMEBREW_INSTALL_FROM_API=1
ENV HOMEBREW_NO_ENV_HINTS=1
ENV HOMEBREW_NO_ANALYTICS=1
ENV BASH_ENV=${ENV_FILE}

RUN apt-get update && \
    apt-get --yes --no-install-recommends install \
    build-essential \
    ca-certificates \
    curl \
    file \
    git \
    procps && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && \
    brew install \
    gcc && \
    brew cleanup --prune=all

RUN echo "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)\n$(cat ${ENV_FILE})" > ${ENV_FILE}

ENTRYPOINT ["/bin/bash", "-c"]
