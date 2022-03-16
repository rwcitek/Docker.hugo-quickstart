FROM golang:latest

MAINTAINER Robert Citek robert.citek@gmail.com

# setup environment
RUN     DEBIAN_FRONTEND=noninteractive && \
        apt-get update && \
        apt-get dist-upgrade -y && \
        apt-get install -y curl wget git tree vim zip unzip file net-tools

# download/install Hugo
WORKDIR /root/hugo
RUN     curl -L -s -O https://github.com/gohugoio/hugo/releases/download/v0.93.2/hugo_0.93.2_Linux-64bit.tar.gz && \
        tar -xzf hugo_0.93.2_Linux-64bit.tar.gz && \
        mv hugo /usr/local/bin/ && \
        rm hugo_0.93.2_Linux-64bit.tar.gz
WORKDIR /work
RUN     hugo new site quickstart
WORKDIR /work/quickstart

# Add a Theme
RUN     cd /tmp/ && \
        curl -L -O https://github.com/theNewDynamic/gohugo-theme-ananke/archive/master.zip ; \
        unzip master.zip && \
        rm master.zip
RUN     mv /tmp/gohugo-theme-ananke-master ./themes/ananke && \
        echo theme = \"ananke\" >> config.toml

# Add some content
RUN     hugo new posts/my-first-post.md
RUN     sed -i -e '/^draft:/s/true/false/' ./content/posts/my-first-post.md

# finish up
CMD     /usr/local/bin/hugo server --bind 0.0.0.0 -D

COPY    Dockerfile /
