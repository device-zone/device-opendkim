# device-opendkim
Provides an OpenDKIM appliance.

This appliance does the following:

- Automatically configures OpenDKIM's configuration files before startup.
- Binds securely to the unix domain socket /run/opendkim/opendkim.sock.
- Optionally adds domains, selectors and keys to the configuration.
- Autostarts on server restart.

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

