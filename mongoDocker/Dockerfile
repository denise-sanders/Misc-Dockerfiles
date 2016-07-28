# EXPLANATION: Ian: "Your scientists were so preoccupied with whether or not they could, they didn’t stop to think if they should." I made this when I was new to containers and I thought it would be good to give everything a container. I also didn't know a lot about databases. Anyway I am happy to say that I have learned about both and will warn you that it is NOT super smart to put a database server in a container, because it could crash or something else. THere are a lot of tutorials for how to Dockerize databases; these containers are probably being used for testing or something.   


# Dockerizing MongoDB: Dockerfile for building MongoDB images
# Based on ubuntu:latest, installs MongoDB following the instructions from:
# http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

# This is the image docker will run in!
# Format: FROM    repository[:version]
FROM       ubuntu:latest

# Format: MAINTAINER Name <email@addr.ess>
MAINTAINER Denise Irvin <denise.irvin@rackspace.com>

# Installation:
# Import MongoDB public GPG key AND create a MongoDB list file
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10
#RUN echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.0.list
RUN echo "deb http://repo.mongodb.org/apt/debian wheezy/mongodb-org/3.0 main" | tee /etc/apt/sources.list.d/mongodb-org-3.0.list

# Update apt-get sources AND install MongoDB
RUN apt-get update && apt-get install -y mongodb-org

# Create the MongoDB data directory
RUN mkdir -p /data/db

# Expose port 27017 from the container to the host
EXPOSE 27017

ENTRYPOINT ["/usr/bin/mongod"]
