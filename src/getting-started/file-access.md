# File Access

Accessing your µLab files necessitates a file-transfer client that
supports the SSH protocol.  Although there are a lot of clients to
choose from, we'll cover a few of the most popular options.


## SCP

OpenSSH secure file copy (`scp`) is a command that behaves much like the
`cp` command with the added bonus of working over SSH.  The command has
the following semantics:

```
$ scp [OPTIONS] source ... target
```

Lets say you want to download a file called `homework.c` under
`~/cu/ece-160/` to your local directory, the command would be as
follows:

```
$ scp -P 31415 first.last@dev.ee.cooper.edu:cu/ece-160/homework.c .
(first.last@dev.ee.cooper.edu) Password:
homework.c                            100% 1247    60.8KB/s   00:00
$ _
```

Or lets say you wanted to copy a file called `project.c` in your local
directory to the folder `~/cu/ece-160/`:

```
$ scp -P 31415 project.c first.last@dev.ee.cooper.edu:cu/ece-160
(first.last@dev.ee.cooper.edu) Password:
project.c                    100% 3102   140.7KB/s   00:00
$ _
```

And if you want to move a directory, you'll have to run the command
recursively with the `-r` flag:

```
$ scp -r -P 31415 first.last@dev.ee.cooper.edu:cu/ece-160 .
(first.last@dev.ee.cooper.edu) Password:
homework.c                    100% 1247    74.2KB/s   00:00
project.c                     100% 3102   167.6KB/s   00:00
lesson-0.md                   100% 2783   135.9KB/s   00:00
assignment-0.md               100% 1492    76.1KB/s   00:00
...
$ _
```

> Note that if you added µLab hosts to your [SSH configuration] the
> commands above could have been simplified down to the following:
>
> ```
> $ scp dev.ee.cooper.edu:cu/ece-160/homework.c .
> $ scp project.c dev.ee.cooper.edu:/tmp
> $ scp -r @dev.ee.cooper.edu:cu/ece-160 .
> ```


[SSH configuration]: ssh.md#adding-an-ssh-configuration
