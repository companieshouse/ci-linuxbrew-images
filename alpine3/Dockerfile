FROM alpine:3

ENV HOMEBREW_NO_ENV_HINTS=1
ENV HOMEBREW_NO_ANALYTICS=1

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

RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)" && \
    echo "eval \"\$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)\"" >> ~/.bash_profile

RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && \
    brew install \
    gcc && \
    brew cleanup --prune=all

ENTRYPOINT ["/bin/bash", "-l"]
