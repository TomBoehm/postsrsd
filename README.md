About
=====
This is a fork of Timo Röhlings postsrsd
https://github.com/roehling/postsrsd

This version should compile on Mac OS X.
Tested only with Version 10.9.5

For your convenience I've added the binary 'postsrsd'

Installation on Mac OS X Server
=====

Copy `postsrsd` to `/usr/local/sbin/postsrsd`

Generate a secret by 
    sudo uuidgen > /etc/postsrsd.secret
or write the secret of your chouice to /etc/postsrsd.secret
then `chmod 600 /etc/postsrsd.secret`

Modify `/Library/Server/Mail/Config/postfix/main.cf` as described at roehling/postsrsd and add

    sender_canonical_maps = tcp:127.0.0.1:10001
    sender_canonical_classes = envelope_sender
    recipient_canonical_maps = tcp:127.0.0.1:10002
    recipient_canonical_classes= envelope_recipient

Start postsrsd
    /usr/local/sbin/postsrsd -s /etc/postsrsd.secret -d mydomain.com -f 10001 -4 -X my-second-domain.com

you should generate a LaunchDaemon for this command
