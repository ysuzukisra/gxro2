FROM ubuntu:16.04

RUN set -x && \
    apt-get update && \
    ###
    ### Docker 導入
    ###
    apt-get install -y --no-install-recommends \
      apt-transport-https \
      wget \
      software-properties-common \
      ca-certificates \
      && \
    wget -q 'https://keyserver.ubuntu.com/pks/lookup?op=get&search=0xee6d536cf7dc86e2d7d56f59a178ac6c6238f52e' -O - \
      | apt-key add - \
      && \
    add-apt-repository "deb https://packages.docker.com/1.13/apt/repo/ ubuntu-$(lsb_release -cs) main" && \
    apt-get update && \
    apt-get install -y docker-engine && \
    ###
    ### メンテとjenkins-slaveに必要なものを導入
    ###
    apt-get install -y git vim && \
    apt-get install -y openjdk-8-jre && \
    apt-get install -y openssh-client openssh-server && \
    ###
    ### レイヤを軽くする
    ###
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    ###
    ### 終了
    ###
    echo done.

RUN set -x && \
    ###
    ### Docker Compose 導入
    ###
    wget https://github.com/docker/compose/releases/download/1.12.0/docker-compose-`uname -s`-`uname -m` -O /usr/local/bin/docker-compose && \
    chmod +x /usr/local/bin/docker-compose && \
    ###
    ### 終了
    ###
    echo done.

RUN set -x && \
    ###
    ### コンテナ設定
    ###
    echo root:dind | chpasswd && \
    ssh-keygen -A && \
    mkdir /var/run/sshd && \
    ###
    ### 終了
    ###
    echo done.

EXPOSE 22

CMD ["/usr/sbin/sshd", "-o", "PermitRootLogin yes", "-D"]
