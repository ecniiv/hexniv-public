Receive public key to upload, key.pub for example.

```
$ ssh kruptos "sudo mkdir /home/__USER__/.ssh"
$ cat key.pub | ssh kruptos "sudo tee -a /home/__USER__/.ssh/authorized_keys"
```
