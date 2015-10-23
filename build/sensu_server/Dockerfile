FROM      debian:jessie

# See https://github.com/just-containers/s6-overlay
ADD       https://github.com/just-containers/s6-overlay/releases/download/v1.16.0.0/s6-overlay-amd64.tar.gz /tmp/
RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C / && rm /tmp/s6-overlay-amd64.tar.gz

RUN       apt-get update && \
          apt-get install -y redis-server

RUN       apt-get install -y curl && \
          curl http://repositories.sensuapp.org/apt/pubkey.gpg  | apt-key add - && \
          echo "deb     http://repositories.sensuapp.org/apt sensu main" | tee /etc/apt/sources.list.d/sensu.list && \
          apt-get update && apt-get install -y sensu

RUN       apt-get install -y git && \
          git clone http://github.com/opower/sensu-metrics-relay.git && \
          cp -R sensu-metrics-relay/lib/sensu/extensions/* /etc/sensu/extensions

ENTRYPOINT ["/init"]

