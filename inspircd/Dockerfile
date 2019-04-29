FROM alpine AS base
RUN apk add --no-cache --virtual .dependencies libgcc libstdc++ gnutls gnutls-utils perl
RUN addgroup -g 10000 -S inspircd
RUN adduser -u 10000 -h /inspircd -D -S -G inspircd inspircd



FROM base AS build
RUN apk add --no-cache --virtual .build-utils gcc g++ make git pkgconfig \
    perl-net-ssleay perl-crypt-ssleay perl-lwp-protocol-https \
    perl-libwww wget gnutls-dev
USER inspircd
COPY --chown=inspircd:inspircd ./inspircd-git /src
WORKDIR /src
RUN ./configure \
    --development \
    --prefix=/inspircd
RUN make -j"$(nproc)"
RUN make install



FROM base AS run
USER inspircd
WORKDIR /inspircd
COPY --chown=inspircd:inspircd --from=build /inspircd .
RUN rm ./conf -rf
VOLUME /inspircd/conf
CMD ./inspircd start --nofork
