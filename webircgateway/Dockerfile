FROM golang:alpine as build
RUN apk add --no-cache \
    build-base \
    git
WORKDIR /root/
COPY go.mod .
COPY go.sum .
RUN go mod download
COPY . .
RUN make

FROM alpine
RUN apk add --no-cache \
    ca-certificates
WORKDIR /root/
COPY --from=build /root/webircgateway .
COPY --from=kiwiirc-client /root/kiwiirc-client/dist/ ./www/
COPY --from=plugin-olm /root/plugin-olm/dist/ ./www/
EXPOSE 80 443 113
ENTRYPOINT [ "/root/webircgateway" ]
