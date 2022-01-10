FROM centos:8

ENV HOMEBREW_NO_ENV_HINTS=1
ENV HOMEBREW_NO_ANALYTICS=1

RUN yum -y groupinstall 'Development Tools'

RUN yum -y install \
    epel-release \
    git && \
    yum clean all
    
RUN /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"

RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && \
    brew install \
    gcc && \
    brew cleanup --prune=all

RUN echo "eval \"\$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)\"" >> ~/.bash_profile

ENTRYPOINT ["/bin/bash", "-l", "-c"]
