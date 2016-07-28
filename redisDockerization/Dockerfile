# For the Dockerization of redis, to be used with symdash.
# build using sudo docker build -t redis_img .


# Set base image as Trusty Ubuntu
FROM ubuntu:14.04

# File Author / Maintainer
MAINTAINER Team Symetric (Denise)

# Install general things
RUN apt-get update && apt-get install -y \
        gcc \
        libpq-dev \
        npm \
        python \
        python-dev \
        python-pip \
        python-setuptools \
        wget

# Configure Redis
# TODO: figure out how starting services works when creating images
# TODO: come up with something elegant for file permissions
ADD http://download.redis.io/redis-stable.tar.gz /tmp/redis-stable.tar.gz
RUN tar zxf /tmp/redis-stable.tar.gz -C /tmp
RUN make -C /tmp/redis-stable
RUN make install -C /tmp/redis-stable
RUN useradd redis
RUN groupadd redis -f
RUN usermod -g redis redis
RUN touch /var/log/redis.log
RUN mkdir /etc/redis
RUN mkdir /var/db
RUN mkdir /var/db/redis
COPY redis.conf /etc/redis/redis.conf
COPY redis_init /etc/init.d/redis
RUN update-rc.d -f redis defaults
RUN echo 'REDIS_HOME="/etc/redis"' >> /etc/environment
RUN rm /tmp/redis-stable.tar.gz 

EXPOSE 6378

# Works, but we want to use a service
ENTRYPOINT ["usr/local/bin/redis-server"]

# can't find executable, Im not sure if this is what we want
# ENTRYPOINT ["service redis restart"]

