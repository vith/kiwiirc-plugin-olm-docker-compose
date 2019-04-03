FROM node AS build
COPY --from=olm /root/olm/ /root/olm/
WORKDIR /root/olm/javascript/
RUN yarn link

WORKDIR /root/plugin-olm/
COPY package.json .
COPY yarn.lock .
RUN yarn link olm
RUN yarn --frozen-lockfile --no-scripts
COPY . .
RUN yarn --frozen-lockfile
RUN yarn run build-plugin



FROM node
RUN yarn global add serve
WORKDIR /root/plugin-olm/
COPY --from=build /root/plugin-olm/dist/ ./dist/
CMD serve --no-clipboard ./dist/
