FROM centos:8

ARG ENV_FILE="/root/.bashrc"

ENV HOMEBREW_INSTALL_FROM_API=1
ENV HOMEBREW_NO_ENV_HINTS=1
ENV HOMEBREW_NO_ANALYTICS=1
ENV BASH_ENV=${ENV_FILE}

RUN sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-Linux-* && \
    sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-Linux-*

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

RUN echo -e "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)\n$(cat ${ENV_FILE})" > ${ENV_FILE}

ENTRYPOINT ["/bin/bash", "-c"]
