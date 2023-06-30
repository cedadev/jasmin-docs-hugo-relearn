---
aliases: /article/204-interactive-computing-overview
categories:
- Interactive Computing
collection: jasmin-documentation
date: 2022-06-08 12:58:24
description: Interactive computing overview
slug: interactive-computing-overview
title: Interactive computing overview
---

This article introduces the resources on JASMIN available for interactive
computing (as opposed to [batch computing](slurm)). It covers:

  * Login servers
  * Scientific Analysis servers
  * Data Transfer Servers
  * Project Specific Servers

## Login Severs

The [login (also known as gateway or bastion) servers](login-servers) provide
external* users with access to services inside of JASMIN.

*external = outside of the STFC/RAL firewall. 

## Scientific Analysis Servers

The [scientific analysis servers](sci-servers) are the main resource for most
users' everyday work. They have a [standardised software environment](jap) and
are ideal for development and testing of processing tasks which can then be
submitted to the [LOTUS batch processing cluster](slurm) for larger processing
runs.

## Data Transfer Servers

General [data transfer servers](transfer-servers) are provided for simple or
smaller data transfer tasks. For larger data flows or where high performance
is required, more sophisticated tools and services are available. Please read
the guides in consult the [data transfer
category](http://help.ceda.ac.uk/category/217-data-transfer) for more details.

## Project-Specific Servers

In some cases, project requirements are not met by the general resources
provided above and [project-specific servers](project-specific-servers) can be
provided, although in many cases, a [tenancy in the JASMIN
Cloud](http://help.ceda.ac.uk/category/65-for-cloud-tenants) may provide
what's needed.


