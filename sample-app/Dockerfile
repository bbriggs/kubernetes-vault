FROM golang:1.8-alpine as builder

WORKDIR $GOPATH/src/github.com/Boostport/kubernetes-vault

COPY . .

RUN apk --update add gcc git musl-dev \
 && go get -u github.com/Masterminds/glide \
 && glide install --strip-vendor \
 && cd sample-app \
 && go build -o sample-app

FROM alpine:latest
LABEL maintainer Francis Chuang <francis.chuang@boostport.com>

COPY --from=builder /go/src/github.com/Boostport/kubernetes-vault/sample-app/sample-app /sample-app

ENTRYPOINT ["/sample-app"]