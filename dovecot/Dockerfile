FROM dovecot/dovecot:2.3.19.1

COPY dovecot.conf /etc/dovecot/

# https://doc.dovecot.org/configuration_manual/howto/simple_virtual_install/
COPY passwd /etc/dovecot/passwd

ENTRYPOINT ["/usr/sbin/dovecot"]
CMD ["-F"]
