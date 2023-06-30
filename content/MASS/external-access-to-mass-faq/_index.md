---
aliases: /article/231-external-access-to-mass-faq
categories:
- MASS
collection: jasmin-documentation
date: 2023-01-26 15:28:47
description: External Access to MASS FAQ
slug: external-access-to-mass-faq
tags:
- mass partition
- moose
title: External Access to MASS FAQ
---

This article provides answers to MASS frequently asked questions:

  * General 
  * MOOSE messages and what to do 
  * MOOSE basics 

## General

_Can I use my existing MASS account?_

No. You need a separate MASS account for use on the Met Office internal
network (CDN), Monsoon, ECMWF HPCs, and JASMIN. With these different account
types, you can have permission to access different datasets specific to these
computing environments.

_How do I use MOOSE?_

Please see the [MOOSE User Guide here](moose-the-mass-client-user-guide)

_Will my account expire?_

Yes. By default, MASS via JASMIN accounts will expire after 500 days and your
account will be automatically disabled.

Shortly before your account is due to expire you will receive an email, and it
will contain instructions for you and your sponsor about how to extend your
access. If your account has already expired and you are looking to reactive
it, please email: [Monsoon@metoffice.gov.uk](mailto:Monsoon@metoffice.gov.uk)

_Why am I asked for a password when logging in to mass-cli?_

There are two reasons that may result in you being prompted for a password
when attempting to login to the MASS client machine (mass-cli.jasmin.ac.uk).

The first is if you do not have permission to access the machine. A quick
method to check is to verify if you are a member of the moose user group. It
should be listed when you use the ‘groups’ command:

    
    
    [login1]$ groups
    moose
    

If this happens, please contact:
[Monsoon@metoffice.gov.uk](mailto:Monsoon@metoffice.gov.uk)

The second is if you forget the ‘-A’ option when you ssh to a JASMIN login
node. You can test for this condition by listing loaded identities on the
login node, and finding you have none:

    
    
    [login1]$ ssh-add -l
    
    
    
    Could not open a connection to your authentication agent.
    

If this happens, please exit back to your local machine and ssh in again using
the ‘-A’ flag.

_How can I directly login to the MASS client machine?_

No, but you can edit your ssh configuration so that it automatically enables
you to jump through the intermediary login servers.

Add the following to your home institute ssh config file ($HOME/.ssh/config
file):

    
    
    Host mass-cli 
        User your_jasmin_userid 
        HostName mass-cli.jasmin.ac.uk
        ProxyCommand ssh -YA -t your_jasmin_userid@login1.jasmin.ac.uk -W %h:%p 2>/dev/null
    

You should then be able to login directly using:

    
    
     $ ssh mass-cli
    

Please note that this only works if you are using **OpenSSH version 5.4** or
greater as earlier versions do not support the ‘-W’ flag. You can check your
version using: ssh -v

## MOOSE messages and what to do

_"Is this process running in the correct environment?"_

When running 'moo install' you may get an error message similar to:

    
    
     Cannot read file: /home/user/<userid>/.moosedir/moose     
     - is this process running in the correct environment?
    

This can be the result of the wrong combination of Unix user-id and UID having
been used to encrypt the credentials file. If you encounter this error
message, please type `id` on the command line whilst logged into JASMIN, and
send the `uid=` section of the output to:
[Monsoon@metoffice.gov.uk](mailto:Monsoon@metoffice.gov.uk)

Your credentials file will then be reissued.

_Your password is due to expire in X day(s)._

Occasionally on running a MOOSE command you will be told that your password is
due to expire with a message of the form:

    
    
    Your password is due to expire in 6 day(s).   
    A new password can be generated using 'moo passwd -r'.
    

This refers specifically to your MASS via JASMIN, it does not affect any other
MOOSE accounts you may have.

You need to run the command as advised in order to update your credentials
whilst you are logged into mass-cli. You do not actually need to provide a new
password, as this is generated and hidden from you by the command.

If you have a retrieval in progress, it is safe to run this command as it will
not affect processes already running.

## MOOSE basics

_What is MOOSE?_

The software that allows you to interact with MASS.

__

_What is a project?_

A collection of access rules.

__

_What is an access rule?_

Permission to access an area in MASS. For example, project-random might have
an access rule to moose:/crum/random-numbers

Being part of project-random would allow you to access the random-numbers set.

_How do I see what projects I am a member of?_

You can use: `moo prls`

_How do I see what access rules a project has?_

You can use: `moo projinfo -l projectname `

(Replace _projectname_ with the name of one of your projects)

_How do I get access to a project, or add an access rule to one of my
projects?_

Please contact your sponsor. They can then complete this form if they also
agree you require access:

[https://metoffice.service-
now.com/sp?id=sc_cat_item&sys_id=5653331e1bbaf0d88ffa422ad34bcba0&referrer=recent_items](https://metoffice.service-
now.com/sp?id=sc_cat_item&sys_id=5653331e1bbaf0d88ffa422ad34bcba0&referrer=recent_items)

Please note that the link above is only visible to those in the Met Office.

_Why can I not access a set that I know is part of a project?_

If you are given access to a project but do not have access to all the sets
associated with it, this can be due to the Access Control Lists (ACLs).

The project owner will be able to change the ACLs on sets to make them
readable if it is appropriate.

_How do I retrieve a file from MASS?_

Use moo get or moo select. More information about both commands is in the
[MOOSE User Guide](moose-the-mass-client-user-guide).

_How do I make sure my directory has all the available data retrieved from
MASS?_

The problem: You are running a model over a period of several days or weeks,
and you need to analyse the output of the model as it runs. You have a moo get
or moo select command that you run to fetch the data that is available. You
want to be able to re-run it to fetch the files or fields that have been added
to MASS since you last ran the command, but you do not want it to waste time
re-fetching things you already have.

The solution: Use the -i or --fill-gaps option when you run moo get or moo
select. This option tells MOOSE that you only want to fetch files that don't
already exist in the specified local directory. Note that MASS works out where
gaps are by doing checks to see if files of the expected name exist in your
destination directory, so it won't behave correctly if you rename files after
you have retrieved them, or if you use the -C option with moo select which
condenses all the matching fields into a single file.

You might also find the -g / --get-if-available option to moo get useful. This
tells MOOSE to get every file from your moo get list that is available, but
ignore ones that are not there rather than exit with an error. This could help
if you are expecting files to be archived at some point but are not sure
whether they will be there when your job runs. If you use this option MOOSE
will get as much as it can from your list without bailing out.

_How can I script my data retrieval from MASS?_

There are restrictions on how to login to JASMIN and use of Linux utilities
such as ‘cron’ and ‘at’ but it is possible to remotely initiate a retrieval
from MASS on to JASMIN, provided you have your ssh agent running on a machine
local to you.

    
    
    eval $(ssh-agent -s)
    ssh-add ~/.ssh/jasmin_id_rsa 
    ssh -A -X sci1.jasmin.ac.uk 'ssh mass-cli my_script.sh'
    

If you have set up your $HOME/.ssh/config to allow more direct access, then
the following should work:

    
    
    ssh mass-cli my_script.sh
    

This will run the script “my_script.sh” on the MASS client VM. You can put the
moose retrieval commands into a script and it should work:

    
    
    #!/bin/bash 
    SRC_URI=moose:/opfc/atm/global/SOMETHING
    moo get $SRC_URI jasmin_copy.pp 
    exit
    

If you have access to an appropriate JASMIN workspace, then you can scp data
from the workspace directly through one of the dedicated data transfer VMs.
Again, you need the ssh-agent running locally:

    
    
    eval $(ssh-agent -s)
    ssh-add ~/.ssh/jasmin_id_rsa 
    scp userid@xfer1.jasmin.ac.uk:/group_workspaces/cems/<project>/jasmin_file.pp my_local_copy.pp
    

_Can I run MASS retrievals on LOTUS or through a workload manager?_

In addition to the interactive mass-cli server there is also the moose1 server
that is only accessible through the [LOTUS batch cluster](slurm). To submit
jobs to moose1 you must use the [SLURM scheduler](batch-scheduler-slurm-
overview). You will need to specify the account mass and partition mass, for
example:

    
    
    sbatch -A mass -p mass [<options>] <jobscript>
    

where <jobscript> looks something like:

    
    
    #!/bin/bash 
    SRC_URI=moose:/opfc/atm/global/SOMETHING
    moo get $SRC_URI jasmin_copy.pp 
    exit
    

It is also easy to configure the [Rose/Cylc workflow manager](cylc-rose-on-
jasmin) to submit jobs to moose1 through the SLURM scheduler by including the
following lines in your suite.rc file:

    
    
      [[[job submission]]]
          method = slurm
      [[[directives]]]
          --partition=mass
          --account=mass
       [<options>]
    

###


