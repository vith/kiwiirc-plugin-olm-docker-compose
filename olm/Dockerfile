FROM archlinux/base AS build
RUN pacman --noconfirm -Syu --needed base-devel emscripten perl-json cmake jre-openjdk-headless nodejs npm && \
    pacman --noconfirm -Scc
COPY . /root/olm/
WORKDIR /root/olm/javascript/
RUN npm install --no-package-lock
# initialize emcc configs. otherwise it will print a help message instead of building one of the files later!
RUN source /etc/profile.d/emscripten.sh && \
    emcc
RUN source /etc/profile.d/emscripten.sh && \
    npm run build



FROM node
RUN yarn global add serve
WORKDIR /root/olm/
COPY --from=build /root/olm/javascript/ /root/olm/javascript/
EXPOSE 80
CMD serve -l 80 --no-clipboard ./javascript/
