FROM debian

RUN apt-get update -y && apt-get upgrade -y

#DEPENDENCIES
RUN apt-get install git -y
RUN apt-get install wget -y
RUN apt-get install gcc -y

# INSTALL GO
FROM debian:sid

RUN apt-get update && \
	apt-get install --no-install-recommends build-essential ca-certificates \
	git golang-go sqlite libsqlite3-dev openssl openssh-server -y && \
	mkdir -p /root/go/src/github.com/gogits && \
	cd /root/go/src/github.com/gogits && \
	git clone --recurse-submodules -b develop https://github.com/gogits/gogs && \
	cd gogs && \
	go build -v -tags 'sqlite'

ENV USER="root"
WORKDIR /root/go/src/github.com/gogits/gogs
EXPOSE 3000 22
USER root
CMD ["./gogs", "web"]