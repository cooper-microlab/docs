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


## SFTP

OpenSSH secure file transfer (`sftp`) is a client which gives you an
interactive way to transfer files to remote hosts.  To begin an
interactive session type the following:

```
$ sftp -P 31415 first.last@dev.ee.cooper.edu
Connected to dev.ee.cooper.edu.
sftp> _
```

To see a list of commands, type `help`:

```
sftp> help
Available commands:
bye                                Quit sftp
cd path                            Change remote directory to 'path'
chgrp [-h] grp path                Change group of file 'path' to 'grp'
chmod [-h] mode path               Change permissions of file 'path' to 'mode'
chown [-h] own path                Change owner of file 'path' to 'own'
copy oldpath newpath               Copy remote file
cp oldpath newpath                 Copy remote file
df [-hi] [path]                    Display statistics for current directory or
                                   filesystem containing 'path'
exit                               Quit sftp
get [-afpR] remote [local]         Download file
help                               Display this help text
lcd path                           Change local directory to 'path'
lls [ls-options [path]]            Display local directory listing
lmkdir path                        Create local directory
ln [-s] oldpath newpath            Link remote file (-s for symlink)
lpwd                               Print local working directory
ls [-1afhlnrSt] [path]             Display remote directory listing
lumask umask                       Set local umask to 'umask'
mkdir path                         Create remote directory
progress                           Toggle display of progress meter
put [-afpR] local [remote]         Upload file
pwd                                Display remote working directory
quit                               Quit sftp
reget [-fpR] remote [local]        Resume download file
rename oldpath newpath             Rename remote file
reput [-fpR] local [remote]        Resume upload file
rm path                            Delete remote file
rmdir path                         Remove remote directory
symlink oldpath newpath            Symlink remote file
version                            Show SFTP version
!command                           Execute 'command' in local shell
!                                  Escape to local shell
?                                  Synonym for help
sftp> _
```

As an example, lets see how we'd do everything we did with `scp` with
`sftp`:

```
sftp> get cu/ece-160/homework.c .
Fetching /afs/ee.cooper.edu/user/f/first.last/cu/ece-160/homework.c to ./homework.c
homework.c                                            100% 1247    68.5KB/s   00:00
sftp> put project.c cu/ece-160/
Uploading project.c to /afs/ee.cooper.edu/user/f/first.last/cu/ece-160/
project.c                                             100% 1247   137.3KB/s   00:00
sftp> get -R cu/ece-160 .
Fetching /afs/ee.cooper.edu/user/j/jacob.koziej/cu/ece-160/ to ./ece-160
Retrieving /afs/ee.cooper.edu/user/j/jacob.koziej/cu/ece-160
homework.c                                            100% 1247    81.3KB/s   00:00
project.c                                             100% 3102   171.4KB/s   00:00
lesson-0.md                                           100% 2783   251.6KB/s   00:00
assignment-0.md                                       100% 1492   152.7KB/s   00:00
...
sftp> _
```

Once you're done, either type `exit` or press `^D` to quit.

```
sftp> exit
$ _
```


[SSH configuration]: ssh.md#adding-an-ssh-configuration
