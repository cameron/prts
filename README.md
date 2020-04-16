# What?

In short, a simple service deployment system.

`push-to-systemd` is a git post-receive hook and systemd service that, together, install systemd unit files found in the `push-to-systemd` folder of git repositories pushed to the host.

_(Security note: No, this does not give the `git` user direct access to docker or systemctl; the `git` user writes to a push log that the service reads from to initiate builds and unit file installs.)_

# Install

## Prereqs

1. Configure your box [as a git server](https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server). tl;dr from the guide:
```
root > adduser git
root > su git
git > cd
git > mkdir .ssh && chmod 700 .ssh
git > touch .ssh/authorized_keys && chmod 600 .ssh/authorized_keys
```

Then add your public ssh key to `.ssh/authorized_keys`.

2. [Install docker](https://docs.docker.com/install/).

3. [Install entr](https://github.com/eradman/entr).

## Install push-to-systemd

```
root > cd /usr/share
root > git clone --depth 1 -b master https://github.com/cameron/push-to-systemd
root > /usr/share/push-to-systemd/install
```

### Summary of Installed Files
```
/usr/share/push-to-systemd                       # this repo
/usr/share/push-to-systemd/template.git          # a git template w/ our post-receive hook
/etc/systemd/system/push-to-systemd.service      # systemd unit config runs the following...
/usr/bin/push-to-systemd                         # reads post-receive.log and install services
/usr/bin/push-to-systemd.post-receive            # updates post-receive.log, echoes build/status to pusher
/usr/bin/push-to-systemd.configure-git-user      # makes post-receive available to new repos
/var/log/push-to-systemd.post-receive.log        # <repo_path> <date>
```

I did my best to follow the sentiments in `$ man hier` in organizing the above, `/usr/share` being described as the spot for application-specific cross-platform data. I realize it may be a little odd to put a git repo in `/usr/share`, but I think it's a fine solution.  

# Okay, Now What?

```
git @ server > git init my-repo
...
user @ local > git remote add server git@server:/home/git/my-repo
user @ local > git push server <branch>
... some git output and some status output from systemd! ...
```

To avoid `ssh`ing and `git init`ing every time you want to create a new remote repo, there's a script `git-init-remote`; note that it expects you to also have created a symlink from `/home/git/repos` to `/repos` so that you can keep your repo urls nice and short (`git@server:/repos/my-repo`). (This was left out of the install script b/c it's a convenience that not everyone might prefer.)
