# PRTS
_(Git) (P)ost-(R)eceive (T)o (S)ystemd_

Turn any unix box into a git server that, in the post-receive hook, automatically installs/updates systemd files found in the repo, and re/starts the appropriate services.

# Install

```
root @ server > cd /usr/share
root @ server > git clone --depth 1 -b master https://github.com/cameron/prts
root @ server > ./install
```

# Usage

```
git @ server > cd /srv/my-repo; git init; git checkout <master/main> # (or, see the helper git.init-remote)
user @ local ~/src/my-repo > git remote add prod git@server:/srv/my-repo
user @ local ~/src/my-repo > git push prod main
```
