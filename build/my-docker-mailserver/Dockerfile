FROM tvial/docker-mailserver:latest

RUN set -x && \
    # amavis, dkim, dmarc ‚Í•s—v
    sed -i.ORG \
      -e '/^content_filter = smtp-amavis/s/^/#/' \
      -e '/^smtpd_milters = /s/^/#/' \
      -e '/^non_smtpd_milters = /s/^/#/' \
      /etc/postfix/main.cf && \
    sed -i.ORG \
      -e '/_register_start_daemon "_start_daemons_opendkim"/s/_/#_/' \
      -e '/_register_start_daemon "_start_daemons_opendmarc"/s/_/#_/' \
      -e '/_register_start_daemon "_start_daemons_amavis"/s/_/#_/' \
      /usr/local/bin/start-mailserver.sh && \
    echo done.

