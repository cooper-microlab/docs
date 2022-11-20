# VS Code Remote Development

[VS Code] is one of the most popular text editors, and it'd be a shame
if you couldn't use it on µLab hosts if it is your editor of choice.
Thankfully Microsoft provides an easy-to-use [editor extension] that
allows working remotely over SSH without much configuration.  Feel free
to reference the [official guide], as we'll only cover configuration
changes and quirks you may run into while remotely editing on µLab
hosts.

> Before getting started, we *highly* recommend you add µLab hosts to
> your [SSH configuration] to decrease the complexity of connecting!


## Lock Files in `/tmp`

Since we have a federated login for µLab with home directories stored on
a network file system, lock files stored in a user home directory can
cause issues when connecting to hosts.  To avoid this, change the
`remote.SSH.lockfilesInTmp` setting to `true`.


[VS Code]: https://code.visualstudio.com/
[editor extension]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh
[official guide]: https://code.visualstudio.com/docs/remote/ssh-tutorial
[SSH configuration]: ../getting-started/ssh.md#adding-an-ssh-configuration
