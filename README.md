# PRTS: Post-Receive To Systemd

Forget heroku or codebuild; deployment can be as simple as a git hook!

Okay, not really, but for projects where all you want is to deploy a few systemd files,
prts is all you need.

It's just a git hook that looks through your repo for systemd unit files, installs them,
and re/starts the appropriate services.

And a git repo template to make sure that new git repos get the post receive hook by
default.

And a bit of bash to create your git user and configure your box to be a basic git
server.

~~And a bitcoin miner~~ that's all!

# Install

```
root @ server > cd /usr/share
root @ server > git clone --depth 1 -b master https://github.com/cameron/prts
root @ server > ./install
```

# Usage

```
git @ server > cd /srv/my-repo; git init
user @ local ~/src/my-repo > git remote add prod git@server:/srv/my-repo
user @ local ~/src/my-repo > git push prod main
```
