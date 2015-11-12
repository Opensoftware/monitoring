FROM      debian:jessie

# See https://github.com/just-containers/s6-overlay
ADD       https://github.com/just-containers/s6-overlay/releases/download/v1.16.0.0/s6-overlay-amd64.tar.gz /tmp/
RUN       tar xzf /tmp/s6-overlay-amd64.tar.gz -C / && rm /tmp/s6-overlay-amd64.tar.gz

RUN       apt-get install -y gnupg

RUN       gpg --keyserver keys.gnupg.net --recv-keys 803709B6
RUN       gpg -a --export 803709B6 | apt-key add -

RUN       echo "deb http://packages.flapjack.io/deb/v1 trusty main" | tee /etc/apt/sources.list.d/flapjack.list
RUN       apt-get update
RUN       apt-cache policy flapjack
RUN       apt-get install -y flapjack ca-certificates && \
            echo "daemonize no" >> /opt/flapjack/embedded/etc/redis/redis-flapjack.conf

COPY      data/etc/ /etc/

EXPOSE    3080 3081 3071 6380

ENTRYPOINT ["/init"]
