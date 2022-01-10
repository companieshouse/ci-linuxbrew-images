FROM centos:7

ENV HOMEBREW_NO_ENV_HINTS=1
ENV HOMEBREW_NO_ANALYTICS=1

# Needed to update system cURL
ARG CITYFAN_REPO_RPM="https://mirror.city-fan.org/ftp/contrib/yum-repo/city-fan.org-release-2-2.rhel7.noarch.rpm"

RUN yum -y groupinstall 'Development Tools'

RUN yum -y install \
    centos-release-scl \
    epel-release && \
    yum clean all && \
    yum-config-manager --enable rhel-server-rhscl-7-rpms

RUN yum -y install \
    rh-git227 \
    rh-ruby26 \
    which && \
    yum clean all

RUN yum -y install \
    ${CITYFAN_REPO_RPM} && \
    yum -y --enablerepo=city-fan.org update curl && \
    yum clean all

RUN mkdir -p /home/linuxbrew && \
    git clone https://github.com/Homebrew/brew /home/linuxbrew/.linuxbrew

RUN yum -y erase git && \
    ln -s /opt/rh/rh-git227/root/usr/bin/git /usr/bin/git && \
    ln -s /opt/rh/httpd24/root/usr/lib64/libcurl-httpd24.so.4 /usr/lib64/libcurl-httpd24.so.4 && \
    ln -s /opt/rh/httpd24/root/usr/lib64/libnghttp2-httpd24.so.14 /usr/lib64/libnghttp2-httpd24.so.14

RUN eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)" && \
    brew install \
    curl \
    git \
    gcc \
    glibc && \
    brew cleanup --prune=all

RUN /bin/rm -f \
    /usr/bin/git \
    /usr/lib64/libcurl-httpd24.so.4 \
    /usr/lib64/libnghttp2-httpd24.so.14

RUN yum -y erase \
    rh-git227 \
    rh-ruby26 && \
    yum clean all

RUN echo "eval \"\$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)\"" >> ~/.bash_profile

ENTRYPOINT ["/bin/bash", "-l"]
