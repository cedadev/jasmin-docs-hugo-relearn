---
aliases: /article/4998-issue-affecting-data-transfers-using-globus-online
categories:
- Data Transfer
collection: jasmin-documentation
date: 2021-06-18 10:35:49
description: Issue affecting data transfers using Globus Online
slug: issue-affecting-data-transfers-using-globus-online
title: Issue affecting data transfers using Globus Online
---

(June 2021)

This article provides current advice to JASMIN users of Globus Online and
other high-performance transfer methods which use parallel streams.

# The issue

An issue has been affecting some data transfer methods for several months. The
JASMIN team is still investigating the cause and how to address it, but our
current advice is that **transfers to storage other than`/home/users` or
`/gws/smf/` via Globus Online, or via other methods using parallel streams, is
not recommended**. Other methods (bbcp, gridftp) may be OK if single-stream
transfers can be specified. Single-stream methods are unaffected.

Our current understanding is that there may be an underlying network problem
causing data transfer methods involving parallel streams, to suffer poor
performance. As yet the root cause has not been identified.

It affects any transfer which uses parallel streams to **write** to some
(though not all) storage systems at the JASMIN end.

  * transfers to `/home/users` or `/gws/smf` storage seem unaffected
  * transfers to `/gws/pw` and `/gws/nopw` storage are affected, with performance to /gws/nopw storage areas particularly impaired.

**Read** operations are not affected, so you can safely use Globus Online and
other parallel-stream methods for transferring data **from** all storage on
JASMIN.

# What to do for now?

Transfers using methods which can specify single-stream can proceed
unaffected:

  * with `globus-url-copy`, you must omit the `-p N -fast` options which are used to enable parallel-stream transfers (do not simply set N to 1). The `-cc N` (concurrency) option is still safe to use, as this initiates N single-stream transfers, one for each file (as opposed to multiple streams to transfer a single file, which is problematic). Please see [transfers from ARCHER2](transfers-from-archer2) for an example of how to do this, for single and multiple files at once.
  * with `bbcp`, the default number of streams is 4, so you must actively set this to 1 with the `-s` option.

Unfortunately Globus Online does not enable users to specify single-stream-
only (this can only be done for a "managed endpoint", which the JASMIN
endpoint is not), hence our current recommendation not to use this for
transfers to storage other than `/home/users` or `/gws/smf/` .

An alternative for now is to use `rsync` / `scp` / `sftp` which only do single
stream transfers (these are convenient but do not achieve the best performance
over a given route)

Please look out for further updates on this issue and apologies for the
inconvenience meanwhile.

JASMIN Team


