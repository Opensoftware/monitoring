FROM        debian:jessie

ENV         GRAPHITE_VERSION 0.9.12+debian-6

RUN         apt-get update -y && \
            apt-get install -y graphite-web=${GRAPHITE_VERSION} apache2 apache2-mpm-worker libapache2-mod-wsgi && \
            rm /etc/apache2/sites-enabled/000-default.conf

# A workaround to prepare SQLite database from within Dockerfile,
# because the changed location of STORAGE_DIR is not known yet
# (is set in container runtime with another local_settings.py)
RUN         mkdir -p /data/graphite/storage
COPY        data/local_settings.py /etc/graphite/
RUN         graphite-manage migrate --noinput

RUN         adduser --disabled-password --gecos '' graphite && \
            chown -R graphite:graphite /var/log/graphite && \
            chown -R graphite:graphite /data/graphite/storage

COPY        docker-entrypoint.sh /
COPY        data/graphite.conf /etc/apache2/sites-enabled/

VOLUME      /data/graphite/storage

EXPOSE 	    80

ENTRYPOINT  ["/docker-entrypoint.sh"]
CMD         ["graphiteweb"]
