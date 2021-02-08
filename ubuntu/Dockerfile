FROM ubuntu:devel

ARG FIX_ALL_GOTCHAS_SCRIPT_LOCATION
ARG ETC_ENVIRONMENT_LOCATION
ARG CLEANUP_SCRIPT_LOCATION

ADD $FIX_ALL_GOTCHAS_SCRIPT_LOCATION .
ADD $CLEANUP_SCRIPT_LOCATION .

RUN set -o allexport \
    && . ./fix_all_gotchas.sh \
    && set +o allexport \
    && . ./cleanup.sh

