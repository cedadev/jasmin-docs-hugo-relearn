---
aliases: /article/5037-data-transfer-tools-rclone
categories:
- Data Transfer
collection: jasmin-documentation
date: 2022-01-20 10:22:59
description: 'Data Transfer Tools: rclone'
slug: data-transfer-tools-rclone
title: 'Data Transfer Tools: rclone'
---

This article provides information about the rclone data transfer tool. In
particular:

  * what is rclone?
  * installing rclone for yourself on JASMIN.
  * configuring rclone
  * Dos and Don'ts 

## What is rclone?

rclone is a command-line utility which enables access to lots of different
storage systems including object stores and cloud-based storage. It can also
move data between directories act as an SFTP client so could be used to access
files on JASMIN.

It is very well [documented](https://rclone.org/) already, so rather than
repeat that information here, this article highlights aspects relevant to its
use on JASMIN.

Further information will follow in due course as our experience with this tool
develops.

## Installing rclone for yourself on JASMIN

First off, **do not attempt to follow the documented instructions for
installing on Linux**. As a regular user, **you do not have root/administrator
permission and are not permitted to run scripts using sudo**. Normally most
utilities are already installed for you on JASMIN, but in this case you need
to adapt the documented instructions so that you can safely install this in
your OWN home directory. [That may change in the future if this tool proves
useful].

The recommended procedure for installation on JASMIN is as follows:

Fetch and unpack the Linux binary distribution: (in your home directory on an
**xfer** server)

    
    
    curl -O https://downloads.rclone.org/rclone-current-linux-amd64.zip
    unzip rclone-current-linux-amd64.zip
    cd rclone-*-linux-amd64
    

Next, move the `rclone` executable to your own `bin` directory. You may need
to create that directory if it does not exist already, and add it to your
`PATH` environment variable in your `~/.bash_profile` file

    
    
    # only need these if these aren't in place already in your own setup:
    mkdir ~/bin
    export PATH="~/bin:$PATH" # this works "for now" on the command line, but add to your ~/.bash_profile to make the change permanent.
    
    # move the rclone executable
    mv rclone ~/bin/
    
    # make the permissions on the file executable by you
    chmod 700 ~/bin/rclone
    

Note that you will not have installed the man pages, so these will not be
available: please consult the online documentation instead.

## configuring rclone

Configuring rclone is covered in the rclone documentation. Essentially you
need to configure a **"remote"** representing each storage system you want to
interact with. You can then use rclone to manage data between those "remotes".

## DOs and DON'Ts

  * please **DO NOT use the following features on JASMIN** (at least until further notice). Some of these features look useful, but more work is needed to understand if/how they can be used safely on JASMIN without causing problems. 
    * `rclone mount` (mounting a remote as a filesystem) - **DO NOT USE**
    * `rclone rcd` (remote control daemon) - **DO NOT USE**
    * `rclone serve`(serve remote over a protocol) - **DO NOT USE**
  * you should safely be able to use the following, between remotes that you have configured: 
    * `rclone copy`
    * `rclone sync`
    * `rclone lsd`
    * `rclone ls`
    * `..(other basic commands)`

Help on a particular command is found using

    
    
    rclone <command> --help
    

Further examples of useful ways of using rclone on JASMIN will follow...


