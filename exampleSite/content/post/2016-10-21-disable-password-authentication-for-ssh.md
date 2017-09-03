+++
date = "2016-10-21T21:00:36-07:00"
description = ""
tags        = [ "security", "linux" ]
categories  = [ "Linux"]
title = "How to Disable Password Authentication for SSH"
slug = "disable-password-authentication-for-ssh-linux"

+++

If you are already set up to login to your Linux server using SSH key authentication, you can increase the security of your server by disabling password authentication. To disable password authentication for SSH, do the following:

```bash
$ sudo nano /etc/ssh/sshd_config
```

Set the following settings, or change them to "no" if they already exist:

```bash
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
```

Save the file and restart the ssh server:

```bash
$ sudo systemctl restart sshd.service
```

Or on older non-systemd distros:

```bash
$ /etc/init.d/sshd restart
```
