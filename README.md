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

## Build and test


```bash
IMAGE="ubuntu-16-apache-php-5.6"
BASEDIR="$(pwd)"
RSPEC_CMD_TO_RUN="rspec -f documentation spec/spec_helper.rb"

git clone https://github.com/1and1internet/drone-tests.git
git clone https://github.com/1and1internet/${IMAGE}.git

pushd ${IMAGE}

docker build --pull --rm --tag ${IMAGE} .
docker run --rm -i -t -v /var/run/docker.sock:/var/run/docker.sock -v ${BASEDIR}/drone-tests/:/drone-tests/ -v ${BASEDIR}/${IMAGE}/:/mnt/ -e IMAGE=${IMAGE} 1and1internet/ubuntu-16-rspec ${RSPEC_CMD_TO_RUN}

popd
```
