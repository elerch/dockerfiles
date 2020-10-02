# Run slack desktop app in a container
#
# docker run --rm -it \
#	-v /etc/localtime:/etc/localtime:ro \
#	-v /tmp/.X11-unix:/tmp/.X11-unix \
#	-e DISPLAY=unix$DISPLAY \
#	--device /dev/snd \
#	--device /dev/dri \
#	--device /dev/video0 \
#	--group-add audio \
#	--group-add video \
#	-v "${HOME}/.slack:/root/.config/Slack" \
#	--ipc="host" \
#	--name slack \
#	jess/slack "$@"

FROM debian:buster-slim
LABEL maintainer "Emil Lerch <lobo@lerch.org>"

# Firefox-esr because slack login needs to launch a browser
# dunst/dbus-x11 because we need a way to show notifications and I can't figure out
# how to patch dbus sessions through a rootless container yet.
#
# Note this dbus business screws with showing up in the tray, so we will need
# to figure that out
RUN apt-get update && apt-get install -y --no-install-recommends \
	ca-certificates \
	wget \
  libgtk-3-0 \
  libappindicator3-1 \
  libnotify4 \
  libnss3 \
  libxss1 \
  libxtst6 \
  xdg-utils \
  libatspi2.0-0 \
  kde-cli-tools \
  kde-runtime \
  trash-cli \
  libglib2.0-bin \
  gvfs-bin \
  firefox-esr \
  dbus-x11 \
  libxkbfile1 \
  libxdg-basedir1 \
  && \
  wget -nv https://downloads.slack-edge.com/linux_releases/slack-desktop-4.4.3-amd64.deb && \
  dpkg -i *.deb && \
  rm slack-desktop-4.4.3-amd64.deb \
  && apt remove -y wget \
	&& rm -rf /var/lib/apt/lists/* \
  && mkdir /root/.config

COPY mimeapps.list /root/.config

ENV HOME /home/user
RUN useradd --create-home --home-dir $HOME user \
	&& chown -R user:user $HOME
WORKDIR $HOME
USER user

# Yeah, this is weird. For some reason, slack will fail on first run, then
# succeed on the second...
#
# --no-sandbox is needed as electron likes to setup new namespaces, which
# it can't do from within the container
ENTRYPOINT ["/bin/sh", "-c", "/usr/lib/slack/slack --no-sandbox || /usr/lib/slack/slack --no-sandbox"]
