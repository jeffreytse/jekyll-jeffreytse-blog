---
layout: post
title: SSH connection was closed weirdly
author: Jeffrey Tse
categories: computer
tags: linux terminal ssh
---

## What's up?

Recently, I encountered a weird problem. When I used SSH to connect to a
Linux server, the connection was immediately interrupted, and such a
message appeared: `free(): invalid next size (fast)`, screenshot as
below image:

![image](https://user-images.githubusercontent.com/9413601/94004074-b5002f80-fdce-11ea-9ea9-774a614cd4b4.png)

## Troubleshooting

After that, I tried to connect using another Linux computer and still had
the same problem. But when I tried to connect using a Windows computer, it
was able to connect this time. So I believe it is the problem of the SSH
client.

![image](https://user-images.githubusercontent.com/9413601/94095040-752f5b80-fe53-11ea-8a10-cfa7a273350f.png)

Then, I tried to check the SSH client configuration with below command:

```bash
$ vim /etc/ssh/ssh_config
```

I found a suspicious item `SendEnv LANG LC_*` as below image:

![image](https://user-images.githubusercontent.com/9413601/94005258-9ac75100-fdd0-11ea-940f-3d8630b6cfb0.png)

So I commented out the item and tried to connect again, and this time I was
able to connect without interruption immediately. But when I used the Tab
key for auto-complete, it was interrupted immediately with the message
`realloc(): invalid next size` as below image:

![image](https://user-images.githubusercontent.com/9413601/94099494-a6148e00-fe5d-11ea-904c-ff65e73f6fe4.png)

So far, you must have thought that the problem lies in the SSH client, and
it has been reasonably resolved. However, this is not over yet, just imagine,
some SSH clients can connect, while others still have the same problem.
What a crushing thing.

Now we know that this problem is caused by the SSH environment variable, we
still need to check the SSH server configuration with below command:

```bash
$ vim /etc/ssh/sshd_config
```

As expected, there is an item related to environment variables in the server
configuration, it's `AcceptEnv LANG LC_*` as below image:

![image](https://user-images.githubusercontent.com/9413601/94004989-242a5380-fdd0-11ea-91bf-e1cb33d4cc8b.png)

Therefore, the best approach should be making changes of SSH server’s
configuration. Regardless whether the SSH client sends environment
variables, it will not cause the server connection to be interrupted
immediately.

## Conclusion

**Stop accepting locale on the server.** Do not accept the locale environment
variable from your local machine to the server. You can comment out the
`AcceptEnv LANG LC_*` line in the remote `/etc/ssh/sshd_config` file.
Don’t forget to **restart sshd** to reflect the changes .
