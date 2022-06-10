FROM naskio/n8n-python:latest-debian

RUN cd /usr/lib/node_modules/n8n && npm install n8n-nodes-changed
RUN cd /usr/lib/node_modules/n8n && npm install n8n-nodes-updates
RUN cd /usr/lib/node_modules/n8n && npm install n8n-nodes-influxdb
RUN apt update && apt install -y sudo
RUN usermod -aG sudo node
RUN echo "node ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
