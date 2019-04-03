FROM node AS build
WORKDIR /root/kiwiirc-client/
COPY ./repo/package.json .
COPY ./repo/yarn.lock .
RUN yarn --frozen-lockfile --no-scripts
COPY ./repo/ .
RUN yarn --frozen-lockfile
RUN yarn build

FROM node
RUN yarn global add serve
WORKDIR /root/kiwiirc-client/
COPY --from=build /root/kiwiirc-client/dist/ ./dist/
CMD serve --no-clipboard ./dist/
