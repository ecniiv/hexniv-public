# Git, automated deployment

## Server

Create a group for authorized user to push to git directory.
```
groupadd git
usermod -aG git USER
```

The --bare flag creates a repository with no working directory. It's impossible to edit files and commit changes to that directory. In this directory we can do the git push and git pull commands, but we can't commit to.
```
git init --bare /kruptosgraphein.git
```

And we create a deployment foler.
```
mkdir /srv/kruptos
```

This scrtipt is executed when the push from local machine has been completed. `/kruptosgraphein.git/hooks/pot-receive`:
```
#!/bin/bash
TARGET="/srv/kruptos"
GIT_DIR="/kruptosgraphein.git"
BRANCH="main"

while read oldrev newrev ref
do
	# only checking out the master (or whatever branch you would like to deploy)
	if [ "$ref" = "refs/heads/$BRANCH" ];
	then
		echo "Ref $ref received. Deploying ${BRANCH} branch to production..."
		git --work-tree=$TARGET --git-dir=$GIT_DIR checkout -f $BRANCH
	else
		echo "Ref $ref received. Doing nothing: only the ${BRANCH} branch may be deployed on this server."
	fi
done
```

```
chmod +x /kruptosgraphe.in/hooks/post-receive
chgrp -R git /kruptosgraphein.git/
chgrp -R git /srv/kruptos
```

## Local

```
git remote add prod ssh://login@server/kruptosgraphein.git
```

or

```
git remote add prod ssh://kruptos/kruptosgraphein.git
```

Here `kruptos` is defined in my `~/.ssh/config`:
```
Host kruptos
	Hostname xx.xx.xx.xx
	User user
	IdentityFile ~/.ssh/key.pem
	IdentitiesOnly yes
```
