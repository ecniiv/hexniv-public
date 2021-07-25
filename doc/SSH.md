# SSH Keys Authentification

| Algorithm      |   Stantard   |   Ten years   |  Fifty years |
| -------------- |:------------:|:-------------:|:------------:|
| RSA            |  1024 bits   |   3072 bits   |  15360 bits  |
| ECDSA /ED25519 |   160 bits   |    256 bits   |   512 bits   |

## Server

```
mkdir ~/.ssh && chmod 700 ~/.ssh
```

## Remote

```
ssh-keygen -t ed25519
ssh-copy-id -i ~/path/to/key.pub user@server
ssh-agent $BASH 
ssh-add ~/path/to/key
```
