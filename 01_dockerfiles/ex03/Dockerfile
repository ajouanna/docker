FROM golang
# inspiration : https://gogs.io/docs/installation/install_from_source
#

RUN apt-get update && apt-get install -y libpam0g-dev &&\
	mkdir -p $GOPATH/src/github.com/gogits &&\
	cd $GOPATH/src/github.com/gogits &&\
	git clone --depth=1 -b develop https://github.com/gogits/gogs.git &&\
	cd gogs &&\
	echo 'je fais go get ./...' &&\
	go get ./...  &&\
	echo 'je fais go get -u' &&\
	go get -u -tags "sqlite redis memcache" github.com/gogits/gogs &&\
	echo 'je fais go build' &&\
	go build -tags "sqlite redis memcache"  &&\
	adduser --disabled-login --gecos 'Gogs' git &&\
	chmod -R a+rw .	

WORKDIR /go/src/github.com/gogits/gogs
EXPOSE 3000
CMD su git -c "./gogs web"
