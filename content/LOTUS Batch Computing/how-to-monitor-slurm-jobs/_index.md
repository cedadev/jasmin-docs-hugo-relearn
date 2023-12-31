---
aliases: /article/4892-how-to-monitor-slurm-jobs
categories:
- LOTUS Batch Computing
collection: jasmin-documentation
date: 2020-05-20 13:13:23
description: How to monitor SLURM jobs
slug: how-to-monitor-slurm-jobs
title: How to monitor SLURM jobs
---

This article explains how to monitor SLURM jobs It covers:

  * Job information
  * SLURM commands for monitoring jobs 
  * History of jobs
  * Inspection of job output files

## Job information

Information on all running and pending batch jobs managed by SLURM can be
obtained from the SLURM command`squeue`. Note that information on completed
jobs is only retained for a limited period. Information on jobs that ran in
the past is via.`sacct`An example of the output `squeue`is shown below.

```
squeue 
JOBID PARTITION     NAME   USER ST       TIME  NODES NODELIST(REASON)
18957 short-ser     mean   user1  R       0:01      1 host147
18956 short-ser     calc   user2  R      48:38      1 host146
18967      test     wrap   user1  R      14:25      1 host146
```

where the field 'ST' is the job state and the 'TIME' is the time used by the
job.

A batch job evolves in several states in the course of its execution. The
typical job states are defined in Table 1

Table 1: Job states

Job state  |  Description  
---|---  
PD  |  Pending  |  The job is waiting in a queue for allocation of resources  
R  |  Running  |  The job currently is allocated to a node and is running  
CG  |  Completing  |  The job is finishing but some processes are still active  
CD  |  Completed  |  The job has completed successfully  
F  |  Failed  |  Failed with non-zero exit value  
TO  |  Terminated  |  Job terminated by SLURM after reaching its runtime limit  
S  |  Suspended  |  A running job has been stopped with its resources released
to other jobs  
ST  |  Stopped  |  A running job has been stopped with its resources retained  
  
  
# SLURM commands for monitoring jobs

A list of the most commonly used commands and their options for monitoring
batch jobs are listed in Table 2, below:

Table 2. List of important SLURM commands and their options for monitoring
jobs

SLURM Command  |  Description  
---|---  
`squeue ` |  To view information for all jobs running and pending on the cluster  
`squeue --user=username` |  Displays running and pending jobs per individual user  
`squeue --states=PD` |  Displays information for pending jobs (PD state) and their reasons  
`squeues --states=all` |  Shows a summary of the number of jobs in different states  
`scontrol show job JOBID ` |  Shows detailed information about your job (JOBID = job number) by searching the current event log file  
`sacct -b` |  Shows a brief listing of past jobs
`sacct -l -j JOBID ` |  Shows detailed historical job information of a past job with jobID  
  
  
## Inspection of job output files

An example of the job output file from a simple job submitted to SLURM:

```
sbatch -p test  --wrap="sleep 2m"
Submitted batch job 18973  
```

```
scontrol show job 18973
JobId=18973 JobName=wrap
   UserId=fchami(26458) GroupId=users(26030) MCS_label=N/A
   Priority=1 Nice=0 Account=jasmin QOS=normal
   JobState=RUNNING Reason=None Dependency=(null)
   Requeue=1 Restarts=0 BatchFlag=1 Reboot=0 ExitCode=0:0
   RunTime=00:00:08 TimeLimit=01:00:00 TimeMin=N/A
   SubmitTime=2020-05-20T14:10:28 EligibleTime=2020-05-20T14:10:28
   AccrueTime=2020-05-20T14:10:28
   StartTime=2020-05-20T14:10:32 EndTime=2020-05-20T15:10:32 Deadline=N/A
   SuspendTime=None SecsPreSuspend=0 LastSchedEval=2020-05-20T14:10:32
   Partition=test AllocNode:Sid=sci2-test:18286
   ReqNodeList=(null) ExcNodeList=(null)
   NodeList=host147
   BatchHost=host147
   NumNodes=1 NumCPUs=1 NumTasks=1 CPUs/Task=1 ReqB:S:C:T=0:0:*:*
   TRES=cpu=1,mem=128890M,node=1,billing=1
   Socks/Node=* NtasksPerN:B:S:C=0:0:*:* CoreSpec=*
   MinCPUsNode=1 MinMemoryNode=128890M MinTmpDiskNode=0
   Features=(null) DelayBoot=00:00:00
   OverSubscribe=OK Contiguous=0 Licenses=(null) Network=(null)
   Command=(null)
   WorkDir=/home/users/fchami
   StdErr=/home/users/fchami/slurm-18973.out
   StdIn=/dev/null
   StdOut=/home/users/fchami/slurm-18973.out
   Power=
```    

##

## History of jobs

    
```
sacct
        JobID    JobName  Partition    Account  AllocCPUS      State ExitCode 
------------ ---------- ---------- ---------- ---------- ---------- -------- 
18963              wrap par-single     jasmin          1  COMPLETED      0:0 
18964              wrap short-ser+     jasmin          1  COMPLETED      0:0 
18965              wrap par-single     jasmin          1  COMPLETED      0:0 
18966              wrap short-ser+     jasmin          1  COMPLETED      0:0 
```


