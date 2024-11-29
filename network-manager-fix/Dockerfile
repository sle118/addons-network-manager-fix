ARG BUILD_FROM
FROM $BUILD_FROM

# Setup base
ARG LIBWEBSOCKETS_VERSION
# Setup base
RUN \
    set -x && \
    apk add --no-cache \
        bash-completion \
        pulseaudio-utils \
        alsa-plugins-pulse \
        bluez \
        git \
        libuv \
        mosquitto-clients \
        nano \
        openssh \
        pwgen \
        tmux \
        vim \
        networkmanager \
        networkmanager-cli \
        apparmor-utils

        # Extract NetworkManager version
        # nm_version=$(apk list --installed 2>/dev/null | grep 'networkmanager-' | grep -oE '[0-9]+\.[0-9]+\.[0-9]+' | uniq) && \
        # apk add --no-cache "networkmanager-cli=$nm_version" && \
        # echo "Aligned NetworkManager version: $nm_version"



# Home Assistant CLI
ARG BUILD_ARCH
ARG CLI_VERSION
RUN curl -Lso /usr/bin/ha \
        "https://github.com/home-assistant/cli/releases/download/${CLI_VERSION}/ha_${BUILD_ARCH}" \
    && chmod a+x /usr/bin/ha 



# Copy data
COPY rootfs /


RUN \
    set -x && \
    chmod a+x /usr/bin/nmfix*  &&\
    chmod a+x /etc/s6-overlay/scripts/* &&\
    chmod a+x /etc/s6-overlay/s6-rc.d/nmfix/*