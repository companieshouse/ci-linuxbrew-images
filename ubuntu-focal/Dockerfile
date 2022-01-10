FROM ubuntu:focal

ARG DEBIAN_FRONTEND=noninteractive

ENV HOMEBREW_NO_ENV_HINTS=1
ENV HOMEBREW_NO_ANALYTICS=1

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

RUN echo "eval \"\$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)\"" >> ~/.profile

ENTRYPOINT ["/bin/bash", "-l", "-c"]
