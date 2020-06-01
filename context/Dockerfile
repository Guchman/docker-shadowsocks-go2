FROM golang:1.9.5 AS build

WORKDIR /go

RUN go get -u -v github.com/shadowsocks/go-shadowsocks2

FROM alpine:3.7

RUN apk --no-cache add ca-certificates \
 && wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub \
 && wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.26-r0/glibc-2.26-r0.apk \
 && apk add --no-cache glibc-2.26-r0.apk \
 && rm -rf glibc-2.26-r0.apk

COPY --from=build /go/bin/go-shadowsocks2 /go/bin/go-shadowsocks2

EXPOSE 443

ENTRYPOINT ["/go/bin/go-shadowsocks2"]
CMD ["-s", "ss://AEAD_CHACHA20_POLY1305:1234@:443", "-verbose", "-u"]
