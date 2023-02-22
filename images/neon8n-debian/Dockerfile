FROM nikolaik/python-nodejs:python3.10-nodejs14

# changing user `pn` to `node`
RUN usermod --login node --move-home --home /home/node pn
RUN groupmod --new-name node pn

ARG N8N_VERSION

RUN if [ -z "$N8N_VERSION" ] ; then echo "The N8N_VERSION argument is missing!" ; exit 1; fi

USER node
RUN python -m pip install --upgrade pip setuptools wheel yt-dlp
RUN echo '$PATH=$PATH:/home/node/.local/bin/' >> ~/.bashrc

USER root

RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get -y install graphicsmagick gosu git sudo aria2 ffmpeg python3-pip
RUN usermod -aG sudo node
RUN echo "node ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers


RUN npm_config_user=root npm install -g full-icu n8n@${N8N_VERSION}

# Install n8n-nodes-python module
RUN cd /usr/lib/node_modules/n8n && npm install n8n-nodes-python

ENV NODE_ICU_DATA /usr/lib/node_modules/full-icu

WORKDIR /data

COPY docker-entrypoint.sh /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]

EXPOSE 5678/tcp

RUN cd /usr/lib/node_modules/n8n && npm install n8n-nodes-changed
RUN cd /usr/lib/node_modules/n8n && npm install n8n-nodes-updates
RUN cd /usr/lib/node_modules/n8n && npm install n8n-nodes-influxdb


