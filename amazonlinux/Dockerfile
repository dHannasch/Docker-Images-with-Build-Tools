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
    && yum install --assumeyes https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && yum install --assume-yes git gcc-c++ cmake wget curl \
    && yum install --assume-yes libXt p7zip-plugins unzip \
    && rm --recursive --force /var/cache/yum \
    && . ./cleanup.sh
