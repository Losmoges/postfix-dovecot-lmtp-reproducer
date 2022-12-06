# Postfix Dovecot LMTP Reproducer

This repository demonstrates a question. To see the undesireable behaviour execute the following commands

```shell
# Start the services
docker-compose up --force-recreate --detach --build
sleep 1

# Instruct the client to send an email to bob@domain.my through postfix (configured by client/msmtprc)
# Should result in message "Dec 06 22:24:05 host=postfix tls=off auth=off from=alice@domain.my recipients=bob@domain.my mailsize=66 smtpstatus=250 smtpmsg='250 2.0.0 Ok: queued as 21B023DD17' exitcode=EX_OK"
docker exec postfix-dovecot-lmtp-reproducer-client-1 sh -c 'echo test | msmtp bob@domain.my'

docker exec postfix-dovecot-lmtp-reproducer-postfix-1 postqueue -p
```

The email will be stuck in the queue, with the message "(Host or domain name not found. Name service error for name=dovecot type=A: Host not found, try again)"

The root cause can be traced to the entry virtual_transport in postfix/main.cf. When this is changed to the ip adress of the dovecot service (probably 172.18.0.3), then it will work

# Why?
