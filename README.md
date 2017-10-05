# iceberg

Notes on iceberg, the Sheffield HPC facility.

Improve these notes by [editing them on github](https://github.com/hidelab/iceberg) or [by submitting an issue](https://github.com/hidelab/iceberg/issues).

The official Research Computing Group documentation is http://docs.hpc.shef.ac.uk/en/latest/iceberg/.
This document is intended to be more practical notes particularly guided towards our group's needs.

## Logging in

To access `iceberg` you will need to SSH in.
From the command line:

    ssh -X md1xdrj@iceberg.sheffield.ac.uk
    
Don't use `md1xdrj`, that's my username; you'll have to use yours.
Your username and password are the same one you use to access MUSE, unless you have changed it.

(if you use `ssh` a lot, see [my notes about making it more convenient](ssh.md))

## ShARC

ShARC is the HPC system introduced in 2017.
You can use it by replacing `iceberg` with `sharc` when SSH'ing in:

    ssh -X md1xdrj@sharc.sheffield.ac.uk
    
It's still a bit new.

## Submitting jobs

Use `qsub my-job-script` to submit a job.
There are many parameters (see `man qsub` for the ultimate source of truth).
Iceberg's official documentation is here: http://docs.hpc.shef.ac.uk/en/latest/hpc/scheduler/sge.html

Parameters can be specified either on the `qsub` command line,
or in the shell script itself on a line that begins `#$` (see example below).

## Submitting to the hidelab node

Hide Lab rent a node on iceberg which means that we get exclusive access to it.

To run jobs on the hidelab node use `-P hidelab`in the job parameters.

You can either do this each time you submit a job:

    qsub -P hidelab my-job-script

or you can put the parameters in the top section of the job script itself.
To the top section of your job-script, add

    #$ -P hidelab
    
(using `-P` like this will cause the job to run on the hidelab node if it is available,
otherwise it will run on the general queue)

## What jobs do I have?

`qstat -u $USER` will tell you about the jobs that are either running or waiting to run.
If a job has already finished, it won't appear in this list.

`qtop` shows similar information in more detail and is quite fun.

## What jobs are running on the hidelab node

The node is actually a queue, and you can see what jobs are running, and waiting to run,
like this:

    qstat -q hidelab.q
    
The output of this command requires some interpretation.
It's useful to know that `state` tells you whether something is running, `r`, or waiting, `qw`;
and, `slots` is how many CPU cores have been requested.
    
## Iceberg Storage

I have

`/home/md1xdrj` 10 gigabytes

`/data/md1xdrj` 100 gigabytes

You will have similar directories using your username.

We also have purchased additional storage that Hide Lab can use.
It's available on iceberg in

    /shared/hidelab2
    
(this is some sort of magic automount directory, so it doesn't appear in `ls` and so on until you explcitly `cd` to it or use it)

More information about the difference sorts of storage is available on the [official iceberg filestore page](http://docs.hpc.shef.ac.uk/en/latest/iceberg/filestore.html).
