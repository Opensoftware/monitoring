FROM        debian:jessie

ENV         CARBON_VERSION 0.9.12-3

RUN         apt-get update -y && \
            apt-get install -y graphite-carbon=${CARBON_VERSION} && \
            echo "CARBON_CACHE_ENABLED=true" > /etc/default/graphite-carbon

RUN         adduser --disabled-password --gecos '' graphite

RUN         mkdir -p /data/graphite/whisper && \
            chown -R graphite:graphite /data/graphite

COPY        docker-entrypoint.sh /

VOLUME      /etc/carbon
VOLUME      /data/graphite/whisper

USER	      graphite

ENTRYPOINT  ["/docker-entrypoint.sh"]

EXPOSE      2003 2004 7002 2013 2014

CMD         ["cache"]
