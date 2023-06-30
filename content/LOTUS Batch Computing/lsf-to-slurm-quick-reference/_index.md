---
aliases: /article/4891-lsf-to-slurm-quick-reference
categories:
- LOTUS Batch Computing
collection: jasmin-documentation
date: 2022-10-11 15:15:57
description: SLURM quick reference
slug: lsf-to-slurm-quick-reference
tags:
- scancel
- sbatch
- squeue
- cancel
- kill
- lotus
- spec
- specify
- job
- submission
- submit
- batch
- cluster
- bsub
- bqueues
- bjobs
- bkill
- bmod
title: SLURM quick reference
---

This article shows the SLURM commands and their equivalent to the LSF
scheduler (LSF was replaced by SLURM in September 2020). **Note** **:** The
recording and PPT presentation of the first webinar on transitioning from LSF
to SLURM can be found [here](https://www.ceda.ac.uk/events/transitioning-to-
slurm-webinar)

## The SLURM Scheduler

[SLURM ](https://slurm.schedmd.com/) (formerly known as Simple Linux Utility
for Resource Management or SLURM) is the job scheduler deployed on JASMIN. It
allows users to submit, monitor, and control jobs on the CentOS7 LOTUS sub-
cluster.

**Table 1** Essential LSF/SLURM commands

**LSF** |  **SLURM** |  **Description**  
---|---|---  
bsub < _script_file_ |  sbatch _script_file_ |  Submit a job script to the
scheduler  
bqueues  |  sinfo  |  Show available scheduling queues  
bjobs  |  squeue -u _< username>_ |  List user's pending and running jobs  
  
bsub -n 1 -q test -Is /bin/bash  |  srun -n 1 -p test --pty /bin/bash  |
Request an interactive session on LOTUS  
|  |  
  
**Table 2** Job specification

**LSF** |  **SLURM** |  **Description**  
---|---|---  
#BSUB  |  #SBATCH  |  Scheduler directive  
-q _queue_name_ |  \--partition _=_ _queue_name or_ -p _queue_name_ |  Specify the scheduling queue   
-W _hh:mm:ss_ |  \--time= _hh:mm:ss_ or -t _hh:mm:ss_  
|  Set the maximum runtime limit  
-We _hh:mm:ss_ |  \--time-min= _hh:mm:ss_  
|  Set an estimated runtime  
-J _job_name_ |  \--job-name= _jobname_  
|  Specify a name for the job  
-o _filename,_ -e _filename  
_  
__  
  
  
-oo/-eo _filename_  
|  \--output= _filename_ or __ -o filename, _  
_ \--error= _filename_ or -e ___filename_ _  
_ The default file name is "slurm-%j.out", where the "%j"is replaced by the
job ID  
**For job arrays** , the default file name is "slurm-%A_%a.out", " **%A** " is
replaced by the job ID and " **%a** " with the array index.  
\--open-mode=append|truncate  
  
|  Standard job output and error output. Default append.  
  
  
  
  
Overwrite job error/output files  
  
%J  
%I  
|  %j  
%a  
|  Job ID for -oo/eo filename  
Job array index  
  
-R "rusage[mem= _XXX_ ]"  
|  \--mem= _XXX_ |  Memory XXX is required for the job. Default units are
megabytes  
-J _job_name_ [index_list]  |  \--array= _index  
(e.g. --array=1-10) _ |  specify a job array  
-J _job_name_ [index_list]% _number-of-simultaneous-jobs_ |  \--array=index% _ArrayTaskThrottle_  
_e.g._ \--array _=1-15%4_ will limit the number of simultaneously running
tasks from this job array to 4  
|  A maximum number of simultaneously running tasks from the job array may be
specified using a "%" separator.  
-cwd directory  |  -D, --chdir=<directory> |  Set the working directory of the batch script to < _directory >_ before it is executed.   
-x  |  \--exclusive  |  Exclusive execution mode   
-w ' _dependency_expression_ '  |  \--dependency= _< dependency_list>_ |  Defer the start of this job until the specified dependencies have been satisfied completed   
-n _number-of-cores_ |  \--ntasks= _number-of-cores or -n_ _number-of-cores_ |  Number of CPU cores   
-m <host-group-name> |  \--constraint=" _< host-group-name>_"  |  To select a node with a specific processor model   
  
|  |  
  
**Table 3** Job control commands

**LSF** |  **SLURM** |  **Description**  
---|---|---  
bkill _ <_ _jobid >_ |  scancel < _jobid > _ |  Kill a job  
bjobs -l < _jobid >_ |  scontrol show job < _jobid >_ |  Show details job
information  
  
bmod < _jobid >_ |  scontrol update job < _jobid >_ |  Modify a pending job  
bkill 0  |  scancel --user=< _username >_ |  Kill all jobs owned by a user  
  
|  |  
  
**Table 4** Job environment variables

**LSF** |  **SLURM** |  **Description**  
---|---|---  
$LSB_JOBID  |  $SLURM_JOBID  |  Job identifier number  
$LSB_JOBID  
|  $SLURM_ARRAY_JOB_ID  |  Job Array  
$LSB_JOBINDEX  |  $SLURM_ARRAY_TASK_ID  |  Job array index  
$LSB_JOBINDEX_END  |  $SLURM_ARRAY_TASK_MAX  |  Last index number within a job
array  
$LSB_MAX_NUM_PROCESSORS  |  $SLURM_NTASKS  |  Number of processors allocated  
  
|  |


