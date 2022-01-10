FROM amazonlinux:2

ENV HOMEBREW_NO_ENV_HINTS=1
ENV HOMEBREW_NO_ANALYTICS=1

RUN amazon-linux-extras enable ruby3.0 && \
    yum -y groupinstall 'Development Tools' && \
    yum -y install \
    git \
    procps-ng \
    ruby \
    ruby-irb \
    rubygem-rake \
    rubygem-json \
    rubygems && \
    yum clean all

RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" && \
    echo "eval \"\$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)\"" >> ~/.profile

RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && \
    brew install \
    gcc && \
    brew cleanup --prune=all

ENTRYPOINT ["/bin/bash", "-l", "-c"]
