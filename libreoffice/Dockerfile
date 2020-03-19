# Run Libreoffice in a container

# docker run -d \
#	-v /etc/localtime:/etc/localtime:ro \
#	-v /etc/passwd:/etc/passwd:ro \
#	-u "$(id -u "$USER")":"$(id -g "$USER")" \
#	-v /tmp/.X11-unix:/tmp/.X11-unix \
#	-e DISPLAY=unix$DISPLAY \
#	-v $HOME/slides:/home/user/slides \
#	-e GDK_SCALE \
#	-e GDK_DPI_SCALE \
#	--name libreoffice \
#	jess/libreoffice
#
FROM debian:buster-20200224-slim
# Using debian:buster-slim instead of alpine:3.11
# because we need the libreoffice-gtk3 package that I'm not sure exists on
# alpine
LABEL maintainer "Emil Lerch <lobo@lerch.org>"

ENV HOME=/home/user

RUN apt-get update && apt-get -y install --no-install-recommends \
	libreoffice=1:6.1.5-3+deb10u5 \
  libreoffice-gtk3=1:6.1.5-3+deb10u5 && \
  rm -rf /var/cache/apt && \
	mkdir -p /home/user && \
	chmod 777 /home/user

ENTRYPOINT [ "libreoffice" ]
