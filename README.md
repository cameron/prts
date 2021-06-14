# PRTS: Post-Receive To Systemd

Forget heroku or codebuild; deployment can be as simple as a git hook!

Okay, not really, but for projects where all you want is to deploy a few systemd files,
prts is all you need; installing it on your deploy host will create git repo template that
has a post-receive hook that ensures all systemd files found in the repo are installed and
running. The install script will also make sure your deploy host is configured as a git
server...

# Install

```
root > cd /usr/share
root > git clone --depth 1 -b master https://github.com/cameron/prts
root > ./install
```

# Usage

```
git @ server > cd /srv/my-repo; git init
user @ local ~/src/my-repo > git remote add prod git@server:/srv/my-repo
user @ local ~/src/my-repo > git push prod main
```
