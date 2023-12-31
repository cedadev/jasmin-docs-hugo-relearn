---
aliases: /article/199-introduction-to-group-workspaces
categories:
- Short-term project storage
collection: jasmin-documentation
date: 2021-01-12 09:26:56
description: What is a Group Workspace?
slug: introduction-to-group-workspaces
title: What is a Group Workspace?
---

This article describes the JASMIN project storage provision known as Group
Workspace (GWS). It covers:

  * What is a GWS?
  * Accessing a GWS
  * GWS Management
  * Which data sets are in my GWS?

## What is a Group Workspace (GWS)?

Group Workspaces (GWSs) are portions of disk allocated for particular projects
to manage themselves, enabling collaborating scientists to share network
accessible storage on JASMIN. Users can pull data from external sites to a
common cache, process and analyse their data, and where allowed, exploit data
available from other GWSs and from the CEDA archive.

It is important to understand that these Workspaces are not the same as the
CEDA archive. Data in a GWS can be earmarked for ingestion into the CEDA
archive, but this process should be discussed directly with CEDA, it is not
systematic in any way.

Data within GWSs are the responsibility of the designated GWS manager and
**are not backed up by CEDA** (see below).

## Accessing a GWS

### Where are the GWSs?

Each GWS is found in a directory mounted under `/group_workspaces/jasmin2/`
(PFS), `/gws/nopw/j04/` (SOF), or `/gws/pw/j05/` (PFS).Your GWS will be found
under one of these, e.g. `/gws/nopw/j04/jules` .

GWSs are available on:

  * The transfer servers
  * The general scientific analysis servers
  * The LOTUS cluster
  * Some project-specific servers (if requested by the GWS Manager)

### Requesting access to a GWS

There is a Unix group associated with each GWS to provide convenient access
control. Any JASMIN user can apply for access to a given GWS by following the
links provided in the [list of available
GWSs](https://accounts.jasmin.ac.uk/services/group_workspaces/). The GWS
Manager will need to authorise the request before you are granted access.

Once you have been granted access then the relevant Unix group will be added
to your account. If you are not sure of the group name for your GWS you can
find this by entering the command `groups` to see the names of the groups you
belong to. This name normally has the prefix “gws_".

You should have received the specific GWS location from the CEDA Helpdesk when
you were granted access.

##

## GWS management

Each GWS has a designated manager. See the article on 
[managing a GWS]({{< ref "managing-a-gws" >}}).

### Backup

Please note that data in GWSs are only backed up if the GWS Manager has put
tasks in place to do this. The 
[Elastic Tape service]({{< ref "secondary-copy-using-elastic-tape" >}}) is available to enable to  make a secondary near-line copy of data. Please discuss the details with your GWS Manager.

##

### Recommended directory structure for a GWS

We recommend that a sensible directory structure is set up within your GWS in
order to conventions are used within your GWS:

    
```
<your_gws>/
    users/
        <userid>/   # each user can create their own directory here
    public/         # required if you want to share data via HTTP
    data/
        internal/   # internal/intermediate data
        incoming/   # third-party data brought to the GWS
        output/     # output data generated by project
```

See the GWS etiquette article for more details about GWSs and the [GWS data
sharing via HTTP]({{< ref "share-gws-data-via-http" >}}) article for
information about the use of the `public` directory.


