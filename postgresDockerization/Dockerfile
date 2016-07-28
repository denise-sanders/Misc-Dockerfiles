# The Dockerization of Postgres
# NOT TO BE USED BECAUSED IT IS BAD TO VIRUALIZE YOUR DATABASE (TIL) 
# build using sudo docker build -t postgres_img .
# Not quite working (learned I didnt need this before I got it working)

# Set base image as Trusty Ubuntu
FROM ubuntu:14.04

# File Author / Maintainer
MAINTAINER Denise

# Install general things
RUN apt-get update && apt-get install -y \
        gcc \
        git \
        libpq-dev \
        npm \
        python \
        python-dev \
        python-pip \
        python-setuptools \
        wget


# Get Postgresql Repo for 9.5
COPY postgresql.list /etc/apt/sources.list.d/postgresql.list
RUN wget -qO - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Install Postgresql
RUN DEBIAN_FRONTEND=noninteractive apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        postgresql-client-9.5 \
        postgresql-common \
        postgresql-9.5


# Configure postgresql
RUN mv /etc/postgresql/9.5/main/pg_hba.conf /etc/postgresql/9.5/main/pg_hba.conf.bak
RUN mv /etc/postgresql/9.5/main/postgresql.conf /etc/postgresql/9.5/main/postgresql.conf.bak
COPY pg_hba.conf /etc/postgresql/9.5/main/pg_hba.conf
COPY postgresql.conf /etc/postgresql/9.5/main/postgresql.conf

#RUN useradd postgres

ENTRYPOINT ["/usr/lib/postgresql/9.5/bin/postgres"]
#ENTRYPOINT ["su - postgres -c /usr/lib/postgresql/9.5/bin/postgres"]
#CMD ["/usr/lib/postgresql/9.3/bin/postgres", "-D", "/var/lib/postgresql/9.5/main", "-c", "config_file=/etc/postgresql/9.5/main/postgresql.conf"]
#ENTRYPOINT ["/usr/local/lib/postgresql/9.5/bin/postgres -c /etc/postgresql/9.5/main/postgresql.conf -D /etc/postgresql/9.5/main/pg_hba.conf"]
