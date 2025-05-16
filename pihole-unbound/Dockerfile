ARG PIHOLE_VERSION
FROM pihole/pihole:${PIHOLE_VERSION:-latest}
RUN apk update && apk add --no-cache unbound
COPY lighttpd-external.conf /etc/lighttpd/external.conf 
COPY unbound-pihole.conf /etc/unbound/unbound.conf
COPY 99-edns.conf /etc/dnsmasq.d/99-edns.conf
#RUN unbound-anchor 
#ADD https://www.internic.net/domain/named.cache /etc/unbound/root.hints
RUN unbound-checkconf
RUN mkdir -p /etc/services.d/unbound
COPY --chmod=0755 unbound-run /etc/services.d/unbound/run
COPY custom-entrypoint.sh /custom-entrypoint.sh
RUN chmod +x /custom-entrypoint.sh

ENTRYPOINT ["/custom-entrypoint.sh"]
