# oanhnn/docker-laravel-echo-server

[![Software License](https://img.shields.io/github/license/oanhnn/docker-laravel-echo-server.svg)](LICENSE)
[![Build Status](https://img.shields.io/travis/oanhnn/docker-laravel-echo-server/master.svg)](https://travis-ci.org/oanhnn/docker-laravel-echo-server)
[![Docker Build Method](https://img.shields.io/docker/automated/oanhnn/laravel-echo-server.svg)](https://hub.docker.com/r/oanhnn/laravel-echo-server)
[![Docker Build Status](https://img.shields.io/docker/build/oanhnn/laravel-echo-server.svg)](https://hub.docker.com/r/oanhnn/laravel-echo-server)
[![Docker Pull Counter](https://img.shields.io/docker/pulls/oanhnn/laravel-echo-server.svg)](https://hub.docker.com/r/oanhnn/laravel-echo-server)
[![Docker Star Counter](https://img.shields.io/docker/stars/oanhnn/laravel-echo-server.svg)](https://hub.docker.com/r/oanhnn/laravel-echo-server)

Repository of `oanhnn/laravel-echo-server` Docker image.   
Alpine based [Laravel Echo Server](https://github.com/tlaverdure/laravel-echo-server) image.

## Tags

### Version tags

Image Tag    | Badges
-------------|-------
`v1.0.0`     | [![Docker Image Size](https://img.shields.io/microbadger/image-size/oanhnn/laravel-echo-server/v1.0.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:v1.0.0) [![Docker Image Layers](https://img.shields.io/microbadger/layers/oanhnn/laravel-echo-server/v1.0.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:v1.0.0)
`v2.0.0`     | [![Docker Image Size](https://img.shields.io/microbadger/image-size/oanhnn/laravel-echo-server/v2.0.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:v2.0.0) [![Docker Image Layers](https://img.shields.io/microbadger/layers/oanhnn/laravel-echo-server/v2.0.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:v2.0.0)
`2.1.0`      | [![Docker Image Size](https://img.shields.io/microbadger/image-size/oanhnn/laravel-echo-server/2.1.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:2.1.0) [![Docker Image Layers](https://img.shields.io/microbadger/layers/oanhnn/laravel-echo-server/2.1.0.svg)](https://microbadger.com/images/oanhnn/laravel-echo-server:2.1.0)

### Shared tags

- `latest` - `2.1.0`

## Features

- [x] Base from `node:10-alpine` image
- [x] Install `laravel-echo-server`

## Requirement
- Docker Engine 1.13+

## Usage

### Run laravel-echo-server

Run laravel-echo-server by command

```bash
$ docker run -d -p 6001:6001 -v $(pwd):/app oanhnn/laravel-echo-server
```

### Auto generate config file

- If `/app/laravel-echo-server.json` is exists, it will be loaded
- If `/app/laravel-echo-server.json` isn't exists, it will be generated from default configs with [laravel-echo-server](https://github.com/tlaverdure/laravel-echo-server/blob/master/README.md#configurable-options). 
- If `/app/laravel-echo-server.json` isn't exists and you want it will be generated by another process, 
  please set environment variable `GENERATE_CONFIG` to `false` (default `true`).   
  
  ```bash
  $ docker run -d -p 6001:6001 -v $(pwd):/app -e "GENERATE_CONFIG=false" oanhnn/laravel-echo-server
  ```

### Configure database

Using database be configured by environment variable `LARAVEL_ECHO_SERVER_DB` (default is `redis`). 

- By default, Redis database will be used. You can set Redis config by environment variables:

  ```json
  "databaseConfig": {
    "redis": {
      "host": "REDIS_HOST",
      "port": "REDIS_PORT",
      "keyPrefix": "REDIS_KEY_PREFIX",
      "options": {
        "db": "REDIS_DB_BACKEND"
      }
    },
    "sqlite": {}
  },
  ```

  | Environment variable | Default value       |
  |:---------------------|:--------------------|
  | `REDIS_HOST`         | `redis`             |
  | `REDIS_PORT`         | `6379`              |
  | `REDIS_KEY_PREFIX`   | `laravel_database_` |
  | `REDIS_DB_BACKEND`   | `0`                 |

- You can use SQLite database by set environment variable `LARAVEL_ECHO_SERVER_DB` to `sqlite`. 
  The SQLite file will store in `/app/database/`
  
  ```bash
  $ docker run -d -p 6001:6001 -v $(pwd):/app -e "LARAVEL_ECHO_SERVER_DB=sqlite" oanhnn/laravel-echo-server
  ```

### Override config by environment variables

If some environment variables are existed (allow load `/app/.env` file is found), the following options can be overridden:

| Environment variable | Config key | Note |
|:---------------------|:-----------|:-----|
| `LARAVEL_ECHO_SERVER_AUTH_HOST` | `authHost` | This option will fall back to the `LARAVEL_ECHO_SERVER_HOST` option as the default if that is set. |
| `LARAVEL_ECHO_SERVER_HOST` | `host` | |
| `LARAVEL_ECHO_SERVER_PORT` | `port` | |
| `LARAVEL_ECHO_SERVER_DEBUG` | `devMode` | |

See more about `laravel-echo-server.json` in [here](https://github.com/tlaverdure/laravel-echo-server/blob/master/README.md)

### Run laravel-echo-server sub-commands

```bash
$ docker run --rm -it -v $(pwd):/app oanhnn/laravel-echo-server init
$ docker run --rm -it -v $(pwd):/app oanhnn/laravel-echo-server start
$ docker run --rm -it -v $(pwd):/app oanhnn/laravel-echo-server client:add
$ docker run --rm -it -v $(pwd):/app oanhnn/laravel-echo-server client:remove
```

## Contributing

All code contributions must go through a pull request and approved by a core developer before being merged. 
This is to ensure proper review of all the code.

Fork the project, create a feature branch, and send a pull request.

If you would like to help take a look at the [list of issues](https://github.com/oanhnn/docker-laravel-echo-server/issues).

## License

This project is released under the MIT License.   
Copyright © 2018 [Oanh Nguyen](https://github.com/oanhnn)   
Please see [License File](https://github.com/oanhnn/docker-laravel-echo-server/blob/master/LICENSE) for more information.
