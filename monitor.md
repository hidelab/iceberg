# Monitoring and Inspection

Strace is great for finding out what files the SGE commands are using.

`strace -e open qacct` shows the location of the system-wide accounting file.

## Who can access the hidelab.q ?

`qconf -sq hidelab.q` shows (many) details of the `hidelab.q` including which projects can access it.
In this case, it's the `hidelab` project.

`SGE_SINGLE_LINE=1 qconf -su hidelab` shows the list of users in the hidelab ACL which is associated with the hidelab project.

`qconf -shgrp @hidelab` shows which nodes are associated with the `@hidelab` group (not that interesting).

`man project` may also be useful.

## What is running on this node ?

`qstat -q *@$(hostname).iceberg.shef.ac.uk`

Note that you can replace `$(hostname)` with the name of any node to spy on that instead.

## How many queues are there ?

`qconf -sql`

## Miscellania

`qhost` lists all nodes.

`qhost | awk '{print $2,$3}' | sort | uniq` shows all CPU architectures and CPU counts.
