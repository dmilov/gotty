FROM ubuntu:18.04

RUN apt update && \
    apt install -y curl nodejs npm tar git wget && \
    wget https://golang.org/dl/go1.9.7.linux-amd64.tar.gz && \
    tar -C /usr/local -xvf go1.9.7.linux-amd64.tar.gz && \
    export PATH=$PATH:/usr/local/go/bin && \
    export PATH=$PATH:/root/go/bin && \
    go get github.com/dmilov/gotty

# Base layer image$
FROM photon:3.0

# Install Powershell Core
RUN tdnf install powershell -y
#RUN tdnf install powershell tar wget -y && \
#    wget https://github.com/yudai/gotty/releases/download/v1.0.1/gotty_linux_386.tar.gz && \
#    tar -xf gotty_linux_386.tar.gz && \
#    cp gotty /usr/bin/gotty

COPY --from=0 /root/go/bin/gotty /usr/bin/gotty

ADD https://github.com/krallin/tini/releases/download/v0.18.0/tini /sbin/tini
RUN chmod +x /sbin/tini

ENTRYPOINT ["/sbin/tini", "--"]
