# SSH and iceberg

SSH (Secure Shell) is a very widely used tool that provides terminal access to remote servers.

You can use it [to access iceberg](README.md#logging-in).

Here's some tips on using it more effectively.

Command line options can instead appear in your `~/.ssh/config` file.
With a suitably prepared `config` file, I can access iceberg by typing only `ssh iceberg`.

In my `~/.ssh/config` file I have:

```
Host iceberg
Hostname iceberg.sheffield.ac.uk
User md1xdrj
```

that means that I don't have to supply my username,
and it means I can use the shortname `iceberg` instead of the longname `iceberg.sheffield.ac.uk`.
