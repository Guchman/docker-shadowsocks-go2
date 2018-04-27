FROM golang:1.9.5 AS build

WORKDIR /go

RUN go get -u -v github.com/shadowsocks/go-shadowsocks2


FROM alpine:3.7
COPY --from=build /go/bin/go-shadowsocks2 /go/bin/go-shadowsocks2

EXPOSE 443

ENV USER=user

ENTRYPOINT ["/go/bin/go-shadowsocks2"]
CMD ["-s ss://$USER:$PASSWORD@:443 -verbose", "-verbose"]