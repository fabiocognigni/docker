# Ubuntu 14.04 is base image
FROM ubuntu:14.04

# Install curl
RUN apt-get update
RUN apt-get install -y curl

ADD cacert.pem /opt/cacert.pem

CMD curl --cacert /opt/cacert.pem https://api.saks.com/v3/products/?api_key=xxxxxxxxx
