# iceberg

Notes on iceberg, the Sheffield HPC facility.

Improve these notes by [editing them on github](https://github.com/hidelab/iceberg) or [by submitting an issue](https://github.com/hidelab/iceberg/issues).

## Logging in

To access iceberg you will need to SSH in.
From the command line:

    ssh -X md1xdrj@iceberg.sheffield.ac.uk
    
Don't use `md1xdrj`, that's my username; you'll have to use yours.
Your username and password are the same one you use to access MUSE, unless you have changed it.

## Submitting jobs

Use `qsub my-job-script` to submit a job.
There are many parameters.

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
    
## Iceberg Shared Storage

We also have purchased additional storage that Hide Lab can use.
It's available on iceberg in

    /shared/hidelab2
    
(this is some sort of magic automount directory, so it doesn't appear in `ls` and so on until you explcitly `cd` to it or use it)
