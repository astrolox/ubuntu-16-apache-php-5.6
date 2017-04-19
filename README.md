# Apache with PHP 5.6 on Ubuntu 16.04 LTS (Xenial Xerus)

This image provides a common PHP hosting environment. The intent is for the PHP application itself to be stored in persistent storage wihch is then mounted in to this image at `/var/www`

## Usage

Please note this image is explictly intended to be run as a non-privildged user. Ensure you specify a user id (UID) other than zero when you run it. Running as root will not function.


```bash
UID=999
PORT=80
WEB_ROOT="/var/www/"

docker run -u ${UID}:0 -p ${PORT}:8080 -v ${WEB_ROOT}:/var/www/ 1and1internet/ubuntu-16-apache-php-5.6
```

## Building and testing

A simple Makefile is included for your convience. It assumes you have a docker socket avialable at `/var/run/docker.sock`

To build and test just run `make`.
You can also just `make pull`, `make build` and `make test` separately.

Please see the top of the Makefile for various variables which you may choose to customise. Variables may be passed as arguments, e.g. `make IMAGE_NAME=bob` or `make build BUILD_ARGS="--rm --no-cache"`
