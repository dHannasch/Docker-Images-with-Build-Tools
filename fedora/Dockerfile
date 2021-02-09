FROM fedora:rawhide

ARG FIX_ALL_GOTCHAS_SCRIPT_LOCATION
ARG CLEANUP_SCRIPT_LOCATION

ADD $FIX_ALL_GOTCHAS_SCRIPT_LOCATION .
ADD $CLEANUP_SCRIPT_LOCATION .
# The base image does not have wget or anything, so we need to manually get environment.sh.
COPY environment.sh .

RUN set -o allexport \
    && set -o errexit \
    && . ./fix_all_gotchas.sh \
    && set +o allexport \
    && set -o pipefail \
    && if [ -z ${PROXY_CA_PEM+ABC} ]; then echo 'no PROXY_CA_PEM'; else cp $PROXY_CA_PEM /etc/pki/ca-trust/source/anchors/; fi \
    && update-ca-trust \
    && dnf upgrade-minimal --assumeyes \
    && dnf install --assumeyes curl \
    && dnf install --assumeyes --setopt=install_weak_deps=False git gcc-c++ cmake wget \
    && dnf install --assumeyes --setopt=install_weak_deps=False libXt unzip \
    && dnf install --assumeyes --setopt=install_weak_deps=False p7zip-plugins \
    && dnf clean all \
    && . ./cleanup.sh
