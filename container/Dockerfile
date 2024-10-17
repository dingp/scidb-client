FROM almalinux:9

ENV REFRESHED_AT 2024-10-17

RUN yum clean all \
 && yum -y install epel-release dnf-plugins-core \
 && yum -y upgrade \
 && dnf config-manager --set-enabled crb \
 && yum clean all

RUN yum -y install \
    postgresql vim \
 && yum clean all

RUN curl -LsSO https://r.mariadb.com/downloads/mariadb_repo_setup \ 
 &&  echo "6083ef1974d11f49d42ae668fb9d513f7dc2c6276ffa47caed488c4b47268593  mariadb_repo_setup" | sha256sum -c --status \ 
 && chmod +x mariadb_repo_setup \
 && ./mariadb_repo_setup --skip-check-installed \
 && yum clean all \
 && yum -y install MariaDB-client \
 && yum clean all

RUN echo "name=MongoDB Repository" > /etc/yum.repos.d/mongodb-org-8.0.repo \
 && echo "baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/8.0/$basearch/" >> /etc/yum.repos.d/mongodb-org-8.0.repo \
 && echo "gpgcheck=1" >> /etc/yum.repos.d/mongodb-org-8.0.repo \
 && echo "enabled=1" >> /etc/yum.repos.d/mongodb-org-8.0.repo \
 && echo "gpgkey=https://www.mongodb.org/static/pgp/server-8.0.as" >> /etc/yum.repos.d/mongodb-org-8.0.repo \
 && yum update \
 && yum -y install mongodb-mongosh

ENTRYPOINT ["/bin/bash", "-l", "-c" ]
