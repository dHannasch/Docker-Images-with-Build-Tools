FROM amazonlinux

ARG FIX_ALL_GOTCHAS_SCRIPT_LOCATION
ARG CLEANUP_SCRIPT_LOCATION

ADD $FIX_ALL_GOTCHAS_SCRIPT_LOCATION .
ADD $CLEANUP_SCRIPT_LOCATION .
# The base image does not have wget or anything, so we need to manually get environment.sh.
COPY environment.sh .

RUN set -o allexport \
    && . ./fix_all_gotchas.sh \
    && set +o allexport \
    && yum install --assumeyes git gcc-c++ cmake wget curl \
    && if [ -z ${PROXY_CA_PEM+ABC} ]; then echo 'no PROXY_CA_PEM'; else cp $PROXY_CA_PEM /etc/pki/ca-trust/source/anchors/; fi \
    && update-ca-trust \
    && yum install --assumeyes https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && yum install --assumeyes libXt p7zip-plugins unzip \
    && rm --recursive --force /var/cache/yum \
    && . ./cleanup.sh
