FROM debian:buster

RUN apt-get update \
  && apt-get install -y postfix

COPY main.cf /etc/postfix/main.cf
COPY vmailbox /etc/postfix/vmailbox
RUN postmap /etc/postfix/vmailbox

ENTRYPOINT ["/usr/sbin/postfix"]
CMD ["start-fg"]
