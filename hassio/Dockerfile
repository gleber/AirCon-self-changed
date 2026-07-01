FROM python:3.10

ARG BUILD_VERSION=latest
LABEL io.hass.version="$BUILD_VERSION" io.hass.type="addon" io.hass.arch="armhf|armv7|aarch64|amd64|i386"

RUN apt-get update \
    && apt-get install -y --no-install-recommends jq git \
    && rm -rf /var/lib/apt/lists/*

# Install the patched aircon package from this fork's branch.
RUN pip install --no-cache-dir "git+https://github.com/gleber/AirCon-self-changed.git@local-network-fixes"

ENV PLATFORM=docker
ENV CONFIG_DIR=/config/hisense
ENV OPTIONS_FILE=/data/options.json

COPY run.sh /
RUN sed -i 's/\r$//' /run.sh && chmod a+x /run.sh

CMD [ "bash", "/run.sh" ]
