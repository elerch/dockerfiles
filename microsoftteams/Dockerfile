FROM docker.io/library/debian:buster-20200224-slim

ARG src=https://go.microsoft.com/fwlink/p/?linkid=2112886&clcid=0x409&culture=en-us&country=us

RUN true                                                   \
  && apt-get update                                        \
  && apt-get install --no-install-recommends -y            \
     curl=7.64.0*                                          \
     ca-certificates=20190110                              \
     libpulse0=12.2*                                       \
  && curl -sL "${src}" > /teams.deb                        \
  && apt-get install --no-install-recommends -y /teams.deb \
  && rm /teams.deb                                         \
  && apt-get remove -y curl                                \
  && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/bin/sh", "-c", "/usr/bin/teams; while [ -d /proc/7 ]; do sleep 1; done"]
