FROM ubuntu:20.04

MAINTAINER Robert Citek robert.citek@gmail.com

# based on ...
# https://gohugo.io/getting-started/quick-start/

# source ...
# https://github.com/rwcitek/Docker.hugo-quickstart

# setup environment; useful when interactive or debugging
RUN     DEBIAN_FRONTEND=noninteractive && \
        apt-get update && \
        apt-get dist-upgrade -y && \
        apt-get install -y curl wget git tree vim zip unzip file net-tools

# Step 1: Install Hugo
RUN     DEBIAN_FRONTEND=noninteractive && \
        apt-get update && \
        apt-get install -y hugo

# Step 2: Create a New Site
WORKDIR /work
RUN     hugo new site quickstart

# Step 3: Add a Theme
WORKDIR /work/quickstart
RUN     cd /tmp/ && \
        curl -L -O https://github.com/theNewDynamic/gohugo-theme-ananke/archive/master.zip && \
        unzip master.zip && \
        rm master.zip
RUN     mv /tmp/gohugo-theme-ananke-master ./themes/ananke && \
        echo theme = \"ananke\" >> config.toml

# Step 4: Add Some Content
RUN     hugo new posts/my-first-post.md
RUN     sed -i -e '/^draft:/s/true/false/' ./content/posts/my-first-post.md

# Step 5: Start the Hugo server
CMD     hugo server --bind 0.0.0.0 -D

# finish up
COPY    Dockerfile /


