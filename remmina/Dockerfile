# Run remmina in a container
#
# docker run -d \
#	-v /etc/localtime:/etc/localtime:ro \
#	-v /tmp/.X11-unix:/tmp/.X11-unix \
#	-e DISPLAY=unix$DISPLAY \
#	-v $HOME/.remmina:/root/.remmina \
#	--name remmina \
#	jess/remmina
#
FROM debian:buster-slim
LABEL maintainer "Jessie Frazelle <jess@linux.com>"
RUN true && \
  echo 'deb http://ftp.debian.org/debian buster-backports main' >> /etc/apt/sources.list.d/buster-backports.list && \
  apt-get update && \
	apt-get install -t buster-backports -y \
	hicolor-icon-theme \
	libdbus-1-3 \
	remmina \
	remmina-plugin-rdp \
	remmina-plugin-secret \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

ENV GTK_THEME=Adwaita:dark
ENTRYPOINT [ "remmina" ]
