# HPC: sharc and iceberg

Notes on using the Sheffield High Performance Computing facility. `sharc` and `iceberg`.

Improve these notes by [editing them on github](https://github.com/hidelab/iceberg) or [by submitting an issue](https://github.com/hidelab/iceberg/issues).

The official Research Computing Group documentation is http://docs.hpc.shef.ac.uk/en/latest/iceberg/.
This document is intended to be more practical notes particularly guided towards our group's needs.

`sharc` is the name of the new (as of 2017) HPC facility, it is generally preferred (faster, more reliable, and so on).
`iceberg` is the name of the old facility; it might still be useful to use as it may have more packages installed.

## Logging in

To access `sharc` (or `iceberg`) you will need to SSH in.
From the command line:

    ssh -X md1xdrj@sharc.sheffield.ac.uk
    
Don't use `md1xdrj`, that's my username; you'll have to use yours.
Your username and password are the same one you use to access MUSE, unless you have changed it.

To use `iceberg`, replace `sharc.sheffield.ac.uk` with `iceberg.sheffield.ac.uk`.

(You can make this as short as `ssh sharc`, if you're okay with editing some `ssh` config files, see [my notes about making it more convenient](ssh.md))


## Submitting jobs

Use `qsub my-job-script` to submit a job.
There are many parameters (see `man qsub` for the ultimate source of truth).
Iceberg's official documentation is here: http://docs.hpc.shef.ac.uk/en/latest/hpc/scheduler/sge.html

Parameters can be specified either on the `qsub` command line,
or in the shell script itself on a line that begins `#$` (see example below).

Parameters that you use repeatedly can be place in your `~/.sge_request` file.
I recommend putting at least the following for that file:

    -M your.email@sheffield.ac.uk
    -m e

Other options are probably best set in your script itself.

## Submitting to our queue

On `sharc` Hide Lab have access to the RSE queue (which is a pool of nodes also shared with other groups).
Put `-P rse` in the job parameters.
You can either do this each time you submit a job:

    qsub -P rse my-job-script

or you can put the parameters in the top section of the job script itself.
To the top section of your job-script, add

    #$ -P rse
    
(using `-P` like this will cause the job to run on the rse queue if it is available,
otherwise it will run on the general queue)

On `iceberg` Hide Lab used to rent a node which we could access using `-P hidelab`, but we stopped renting the node in May 2018.

## What jobs do I have?

`qstat` (on `iceberg`:`qstat -u $USER`) will tell you about the jobs that are either running or waiting to run.
If a job has already finished, it won't appear in this list.
This list also includes interactive shell sessions (such as started with `qrshx`), they are jobs that are attached to an interactive terminal.

`qtop` shows similar information in more detail and is quite fun (but it does not work on `sharc`).

## What jobs are running on the RSE nodes

You can inspect a queue (`rse.q` in the _queue_ for the `rse` _project_) like this:

On `sharc`

    qstat -s r -q rse.q -u \*

In the above commands `-s r` means we see only running jobs.
If you want to see other jobs (for example, you can see the priority of your own jobs that are waiting),
you can remove the `-s r` part.

It's useful to know that `state` tells you whether something is running, `r`, or waiting, `qw`;
and, `slots` is how many CPU cores have been requested.
    
## HPC Storage

I have

`/home/md1xdrj` 10 gigabytes

`/data/md1xdrj` 100 gigabytes

You will have similar directories using your username.

We also have purchased additional storage that Hide Lab can use.
It's available on `sharc` (and `iceberg`) in

    /shared/hidelab2
    
This is some sort of magic automount directory, so it doesn't appear in `ls` and so on until you explcitly `cd` to it or use it.

More information about the difference sorts of storage is available on the [official iceberg filestore page](http://docs.hpc.shef.ac.uk/en/latest/iceberg/filestore.html).

You can see if you're using lots of storage with:

    df -h ~
    df -h /data/md1xdrj
    df -h /shared/hidelab2
    
or similar.

## end
