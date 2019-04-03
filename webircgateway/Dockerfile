FROM golang:alpine as build
RUN apk add --no-cache \
    build-base \
    git
WORKDIR /root/
COPY ./repo/go.mod .
COPY ./repo/go.sum .
RUN go mod download
COPY ./repo/ .
RUN make

FROM alpine
WORKDIR /root/
COPY --from=build /root/webircgateway .
COPY --from=kiwiirc-docker-compose_kiwiirc-client /root/kiwiirc-client/dist/ ./www/
COPY --from=kiwiirc-docker-compose_plugin-olm /root/plugin-olm/dist/ ./www/
EXPOSE 80
CMD /root/webircgateway
