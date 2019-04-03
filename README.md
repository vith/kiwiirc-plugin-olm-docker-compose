# kiwiirc-plugin-olm-docker-compose

This repository will build and deploy kiwiirc, webircgateway, plugin-olm, and oragono with docker-compose.

## Usage

```console
$ git submodule update --remote --init
$ docker-compose up
```

## Updating

This will check out the latest commit in each submodule's tracked branch:

```console
$ git pull
$ git submodule update --remote
$ docker-compose build
$ docker-compose up
$ # or:
$ docker-compose up --build
```
