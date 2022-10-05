# device-opendkim
Provides an OpenDKIM appliance.

This appliance does the following:

- All parameters passed to the device commands are syntax checked and canonicalised, with bash completion.
- Automatically configures OpenDKIM's configuration files before startup.
- Binds securely to the unix domain socket /run/opendkim/opendkim.sock.
- Optionally adds domains, selectors and keys to the configuration.
- Autostarts on server restart.
- Zero Trust configuration.

## before

- Deploy the device-opendkim package.

```
[root@server ~]# dnf install device-opendkim
```

- Deploy any RSA keys needed to /etc/pki/tls/private, root only.

```
[root@server ~]# ls -l /etc/pki/tls/private/
total 12
-rw-------. 1 root root  887 Oct  4 11:45 example-dkim.pem
```

## add domains

To add domains, do the following:

```
[root@server ~]# device services mail smtp dkim add domain=example.com selector=default key=example-dkim
```

## enable

To switch the appliance on, run this.

```
[root@server ~]# device services mail smtp dkim enable 
```

## disable

To switch the appliance off, run this.

```
[root@server ~]# device services mail smtp dkim disable  
```

## show dns TXT record

To see the resulting DNS TXT record, run this.

```
[root@server ~]# device services mail smtp dkim show-dns 
default._domainkey.example.com. 86400 IN TXT "v=DKIM1; p=MIGfMA0G[snip]"
```

