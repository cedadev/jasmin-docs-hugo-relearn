---
aliases: /article/3809-data-transfer-tools
categories:
- Data Transfer
collection: jasmin-documentation
date: 2022-01-19 12:25:45
description: Data Transfer Tools
slug: data-transfer-tools
title: Data Transfer Tools
---

This article lists the data transfer tools available on JASMIN and provides
links to articles that describe them in more detail.

## Data Transfer tools

The are many tools that you can use for transferring data to/from JASMIN. See
the articles linked below for more details.

**Tool** |  **Info**  
---|---  
[scp](data-transfer-tools-rsync-scp-sftp)  
|  A basic transfer tool that works over the SSH protocol. Similar to "cp" but
copies between remote servers.  
[rsync (over SSH)](data-transfer-tools-rsync-scp-sftp)  
|  Like scp but slightly more sophisticated. Allows synchronisation between
remote directory trees.  
[sftp](data-transfer-tools-rsync-scp-sftp)  
|  SSH FTP - works over SSH.  
[bbcp](data-transfer-tools-bbcp)  
|  A command-line tool that allows the user to specify parallel transfer over
multiple streams, using SSH authentication.  
[GridFTP (over SSH)](data-transfer-tools-gridftp-ssh-auth) |  A comprehensive
data transfer tool. Highly configurable and able to transfer over multiple
parallel streams. Used over SSH in this case.  
[GridFTP (certificate-based)](data-transfer-tools-gridftp-cert-based-auth)  
|  As above, but using certificate-based authentication instead of SSH
credentials. Efficient for moving large volumes and/or numbers of files,
especially over long distances.  
[Globus Online](data-transfer-tools-globus-command-line-interface)  
|  Managed service for GridFTP, includes capability to orchestrate transfers
between third-party hosts and receive notifications of job status. Has web and
command-line interfaces. Efficient for moving large volumes and/or numbers of
files, especially over long distances.  
[FTP](data-transfer-tools-ftp-and-lftp)  
|  File Transfer Protocol. An aged transfer protocol suitable for small file
transfers but limited.  
[LFTP](data-transfer-tools-ftp-and-lftp)  
|  Parallel-capable FTP client.  
wget, curl  |  Download tools for accessing resources over HTTP primarily.  
See also [sharing GWS data via http](share-gws-data-via-http) for exposing
part(s) of a Group Workspace via HTTP to users without JASMIN accounts.  
  
Python transfer tools  |  Methods of managing/scripting data transfer tasks
using Python. You can use libraries such as `requests` in a Python 3 virtual
environment on the transfer servers.  
[MASS-client (Met Office)](http://help.ceda.ac.uk/category/227-mass)  
|  A specific command-line tool installed on the mass-cli1.ceda.ac.uk server
on JASMIN. Enables extractions from the Met Office MASS Archive directly on to  
OPeNDAP  |  A transfer protocol for extracting subsets of files from a remote
server (over HTTP)  
[bcopy](copy-service)  
|  A parallel transfer tool (specific to JASMIN) that uses the LOTUS batch
cluster to copy data efficiently between disk areas within JASMIN.  
[rclone](data-transfer-tools-rclone)  
|  A 3rd party, open-source command-line utility which can interface to, and
synchronise data between, a wide variety of cloud and other storage backends,
such as Google Drive and AWS S3 compatible object stores. It can also sync
data over SSH.  
This utility is not installed on JASMIN but is well-documented and trivial for
users to download ***** and configure themselves (this should be done on one
of the [data transfer servers](transfer-servers)).  
[ ***** Please see [here](data-transfer-tools-rclone) for further details:
**do not attempt to follow the default install instructions directly on
JASMIN** , as you do not have root or sudo privileges. Also, there are some
limitations on how you should use it on JASMIN.]


