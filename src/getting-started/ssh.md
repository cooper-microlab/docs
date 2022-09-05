# Connecting with SSH

The Secure Shell Protocol, or SSH for short, is your gateway for
accessing µLab resources.  Using SSH, you can conceivably access any of
our resources from anywhere in the world with the bonus of being safe
and secure!


## Invoking the SSH Client

At its most basic level, SSH provides you with a remote shell.  As such,
you will need to utilize a terminal to make a connection.

Open a new terminal or command prompt window and type the following:

```
$ ssh -p31415 first.last@dev.ee.cooper.edu
```

Let's breakdown the command:

* `ssh`: the invocation of the SSH program
* `-p31415`: if you're trying to connect outside of the Cooper network,
  you'll need to manually specify port `31415` as the school's firewall
  blocks SSH's default port
* `first.last`: your µlab username
* `dev.ee.cooper.edu`: the host which we are trying to connect (this can
  be any valid hostname running an SSH daemon)

If you're connecting for the first time to a machine, you might have to
accept the host's key fingerprint:

```
$ ssh -p31415 first.last@dev.ee.cooper.edu
The authenticity of host '[dev.ee.cooper.edu]:31415 ([199.98.27.254]:31415)' can't be established.
ED25519 key fingerprint is SHA256:w1duK0IPo7QWWBInuQKk7fdoYefMvi1SAZ8giVmDVQA.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? _
```

All you need to do here is to type `yes`.

There's some very clever cryptography working behind the scenes to
ensure your connection is secure.  The math governing this is far beyond
the scope of this short guide, but it is here to prevent what's called a
"man-in-the-middle attack."  If a malicious entity were to intercept
your SSH connection, you might see the following if you were to try
connecting again:

```
$ ssh -p31415 first.last@dev.ee.cooper.edu
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ED25519 key sent by the remote host is
SHA256:someMaliciousKeyOverHereDontTryConnecting11.
Please contact your system administrator.
Add correct host key in /home/user/.ssh/known_hosts to get rid of this message.
Offending RSA key in /home/user/.ssh/known_hosts:1
Host key for [dev.ee.cooper.edu]:31415 has changed and you have requested strict checking.
Host key verification failed
$ _
```

If you see this message above when you attempt to connect, and you don't
know for sure that the host key fingerprints have changed, **DO NOT
ATTEMPT TO CONNECT!**  Instead, try to move to a different network
connection to see if that resolves the issue.  If this persists, please
reach out to [`<eeadmin@cooper.edu>`].


## Adding an SSH Configuration

Having to type such a long command can become tiring quite fast.  Using
a non-standard SSH port also creates the annoying situation of having to
manually specify the port for each program that uses SSH internally.  If
only we could avoid this headache!

To avoid this conundrum, you'll need to add a few things to your SSH
configuration file.  This file is located at `~/.ssh/config` on
UNIX-like operating systems and `%USERPROFILE%\.ssh\config` (typically
`C:\Users\username\.ssh\config`) on Windows . Open this file in a text
editor of your choice and add the following:

```
Host *.ee.cooper.edu
	User first.last
	Port 31415
```

After the addition of these lines, you'll be able to connect using SSH
like so:

```
$ ssh dev.ee.cooper.edu
```

Let's say you wanted to type even less because you often SSH into the
remote development machine.  You can add a host alias to your SSH
configuration file like so:

```
Host dev
	Hostname dev.ee.cooper.edu
	User first.last
	Port 31415
```

Now all you'd need to type to SSH to the remote development machine
would be:

```
$ ssh dev
```


[`<eeadmin@cooper.edu>`]: mailto:eeadmin@cooper.edu
