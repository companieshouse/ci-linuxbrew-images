FROM alpine:3

ARG ENV_FILE="/root/.bashrc"

ENV HOMEBREW_NO_ENV_HINTS=1
ENV HOMEBREW_NO_ANALYTICS=1
ENV BASH_ENV=${ENV_FILE}

# Homebrew won't work with Alpine's latest Ruby
ARG APK_REPO_VER="3.11"
ARG RUBY_PKG_VER="2.6.8"

RUN echo "https://dl-cdn.alpinelinux.org/alpine/v${APK_REPO_VER}/main" >> /etc/apk/repositories && \
    echo "https://dl-cdn.alpinelinux.org/alpine/v${APK_REPO_VER}/community" >> /etc/apk/repositories

RUN apk add --no-cache --upgrade \
    bash \
    coreutils \
    curl \
    gcc \
    gcompat \
    git \
    grep \
    procps \
    ruby~=${RUBY_PKG_VER} \
    ruby-bigdecimal~=${RUBY_PKG_VER} \
    ruby-etc~=${RUBY_PKG_VER} \
    ruby-fiddle~=${RUBY_PKG_VER} \
    ruby-io-console~=${RUBY_PKG_VER} \
    ruby-irb~=${RUBY_PKG_VER} \
    ruby-json~=${RUBY_PKG_VER}

RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && \
    brew install \
    gcc && \
    brew cleanup --prune=all

RUN echo -e "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)\n$(cat ${ENV_FILE})" > ${ENV_FILE}

ENTRYPOINT ["/bin/bash", "-c"]
