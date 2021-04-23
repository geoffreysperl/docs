---
slug: how-to-enable-ssh-on-linux
author:
  name: Linode Community
  email: docs@linode.com
description: 'A how to guide for enabling SSH (and understanding it is enabled by default on a Linode) on Linux using OpenSSH and Ubuntu 20.10 on a Linode as the example.'
keywords: ['ssh','openssh','linux','enable ssh linux','enable openssh linux']
tags: ["ssh"]
license: '[CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0)'
published: 2021-04-21
modified_by:
  name: Linode
title: "How to Enable SSH on Linux"
h1_title: "How to Enable SSH on Linux."
contributor:
external_resources:
- '[OpenSSH Project](http://www.openssh.com/)'
- '[OpenSSH Manual Pages](http://www.openssh.com/manual.html)'
---
When we read or hear "SSH," it's usually referring to connecting to a remote server over the SSH protocol and powered by the [OpenSSH open source server and client project](http://www.openssh.com/). When you create a Linode, SSH is enabled by default (even if you use Arch Linux), and you can log in via SSH immediately after it's created and powered on. However, if something happens that you uninstall OpenSSH, if an update goes awry and breaks SSH or something else requires reinstalling and enabling SSH on your Linode (or you need to enable SSH on another machine), here are the steps to do it in Ubuntu (and should be easily adapted to other Linux flavors).

{{< note >}}
This guide is written for a non-root user. Commands that require elevated privileges are prefixed with `sudo`. If you’re not familiar with the `sudo` command, see the [Users and Groups](/docs/tools-reference/linux-users-and-groups/) guide.
{{< /note >}}

## Before You Begin

1.  Familiarize yourself with our [Getting Started](/docs/getting-started/) guide and have a Linode running (or have another Linux system you are using).

2.  This guide will use `sudo` wherever possible. Complete the sections of our [Securing Your Server](/docs/security/securing-your-server/) to create a standard user account, harden SSH access and remove unnecessary network services.

3.  This guide assumes you have access to a command prompt on the Linux system.

4.  Update your system by entering `sudo apt-get update && sudo apt-get upgrade` (or using the appropriate package manager for your flavor of Linux).

## Enabling SSH on Linux

The OpenSSH server is not installed by default in Ubuntu. To install it:

1.  Open the terminal if you are in the graphical environment.

2.  At the command prompt, enter `sudo apt install openssh-server`.

3.  Enter your password if prompted.

4.  Enter `Y` if you are asked if you want to continue. The prompt will look like this:

    {{< output >}}
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  openssh-client openssh-sftp-server ssh-import-id
Suggested packages:
  keychain libpam-ssh monkeysphere ssh-askpass molly-guard
The following NEW packages will be installed:
  openssh-client openssh-server openssh-sftp-server ssh-import-id
0 upgraded, 4 newly installed, 0 to remove and 0 not upgraded.
Need to get 1,062 kB of archives.
After this operation, 5,844 kB of additional disk space will be used.
Do you want to continue? [Y/n]
{{< /output >}}

5.  Make sure the SSH service is working by entering `sudo systemctl status ssh`. Your output should look something like this (especially important is the third line, which states `Active: active (running)`; if the SSH server were off, it would read `Active: inactive (dead)`):

    {{< output >}}
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2021-04-22 14:27:27 EDT; 2min 9s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 452235 (sshd)
      Tasks: 1 (limit: 9410)
     Memory: 1.1M
     CGroup: /system.slice/ssh.service
             └─452235 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups

Apr 22 14:27:27 ubuntu-test systemd[1]: Starting OpenBSD Secure Shell server...
Apr 22 14:27:27 ubuntu-test sshd[452235]: Server listening on 0.0.0.0 port 22.
Apr 22 14:27:27 ubuntu-test sshd[452235]: Server listening on :: port 22.
Apr 22 14:27:27 ubuntu-test systemd[1]: Started OpenBSD Secure Shell server.
{{< /output >}}

6.  The SSH server is now enabled on your Linux system.
    -   If you need to stop the SSH server, enter `sudo systemctl stop ssh`.
    -   If you need to restart the SSH server, enter `sudo systemctl restart ssh`.
    -   If you need to check what the status is, enter `sudo systemctl status ssh`.

7.  Enter `q` to return to the command prompt.

## Enabling SSH on Your Linode

So, you somehow broke SSH on your Linode (no judgment—these things happen). There is a [guide for troubleshooting that](/docs/guides/troubleshooting-ssh/), but you will need to reinstall it if you uninstalled it. To do so, use the instructions above, but use the *Linode Shell* (or "Lish"; see our [guide on using Lish](https://www.linode.com/docs/platform/manager/using-the-linode-shell-lish/)) in the Linode Manager to get to the command prompt.

## Further Reading

Enabling SSH is only the first step. From here, review multiple articles:

-   Learn how to connect to your system over SSH. See the instructions for connecting from your desktop operating system in the ["SSH" section of the guides](docs/guides/networking/ssh/).

-   Learn how to set up [public key authentication over SSH](/docs/guides/use-public-key-authentication-with-ssh/) to restrict logins to specific machines.

-   Learn to secure the system even further by with both "Harden SSH Access" in [How to Secure Your Server](https://www.linode.com/docs/guides/securing-your-server/#harden-ssh-access) and [Use Advanced OpenSSH Features to Harden Access to Your Linode](https://www.linode.com/docs/guides/advanced-ssh-server-security/).