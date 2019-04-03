FROM node AS build
COPY --from=kiwiirc-docker-compose_olm /root/olm/ /root/olm/
WORKDIR /root/olm/javascript/
RUN yarn link

WORKDIR /root/plugin-olm/
COPY ./repo/package.json .
COPY ./repo/yarn.lock .
RUN yarn link olm
RUN yarn --frozen-lockfile --no-scripts
COPY ./repo/ .
RUN yarn --frozen-lockfile
RUN yarn run build-plugin



FROM node
WORKDIR /root/plugin-olm/
RUN yarn global add serve
COPY --from=build /root/plugin-olm/dist/ ./dist/
CMD serve --no-clipboard ./dist/
