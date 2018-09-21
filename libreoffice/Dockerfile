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
FROM alpine:latest
LABEL maintainer "Jessie Frazelle <jess@linux.com>"

ENV HOME=/home/user

RUN apk --no-cache add \
	--repository https://dl-3.alpinelinux.org/alpine/edge/testing \
	libreoffice \
	ttf-dejavu && \
	mkdir -p /home/user && \
	chmod 777 /home/user

ENTRYPOINT [ "libreoffice" ]
