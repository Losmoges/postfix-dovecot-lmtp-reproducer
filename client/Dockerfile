FROM debian:buster

RUN apt-get update && apt-get install --yes msmtp

COPY msmtprc /root/.msmtprc

CMD tail -f /dev/null
