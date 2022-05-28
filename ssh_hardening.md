# SSH Hardening

## New User

This will be done as root

```shell
$ sudo adduser username
```

- Sudo privilege

  ```shell
  $ sudo usermod -aG sudo username
  ```



## Copy public key to new user

This will be done on local

```shell
$ ssh-copy-id -i identity_file username@server_ip
```

Note: You can generate ssh keys using `ssh-keygen` 

```shell
$ ssh-keygen -t rsa -b 4096
```



Note: All of the following steps will be on server, steps to be done on local will be marked local

Note: all of the changes will be done in `/etc/ssh/sshd_config`

## Backup config file

```shell
$ cp /etc/ssh/sshd_config /etc/ssh/sshd_config_bak
```



## Change Port

Uncomment `Port` and change it from `22` to port of your choice

```
#Port 22
```

```
Port {any port}
```



## Disable root login

Note: Make sure you have a non-root user

In `Authentication` change `PermitRootLogin` to `no` 

```
PermitRootLogin no
```



## Limit Max Authentication method

Uncomment `MaxAuthTries` and `MaxSessions` 

```
MaxAuthTries 6
MaxSessions 10
```



## Disable password authentication

Note: Make sure you have copied your public key to server (Follow step 2)

```
PasswordAuthentication no
```

## Configure idle timeout

Note: timeout is in seconds

```
ClientAliveInterval 300
```



Save config file and restart sshd service

```shell
$ service sshd restart
```

