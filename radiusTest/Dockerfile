FROM freeradius/freeradius-server:latest
RUN apt update
RUN apt-get update -y
RUN apt-get install net-tools -y && apt-get install vim -y
COPY raddb/ /etc/raddb/
