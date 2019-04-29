FROM vith/archlinux-olm-build-deps AS build

COPY . /root/olm/
WORKDIR /root/olm/javascript/
RUN npm install --no-package-lock
RUN source /etc/profile.d/emscripten.sh && \
    npm run build



FROM node
RUN yarn global add serve
WORKDIR /root/olm/
COPY --from=build /root/olm/javascript/ /root/olm/javascript/
EXPOSE 80
CMD serve -l 80 --no-clipboard ./javascript/
