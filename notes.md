
- use git push -o tail to leave the service build/logs open
- systemd.path instead of tail
  - do away with githook entirely?
    - but what about logs and output?
      - keep hook, give git journalctl access -- uncouple the git hook and service
        - obviates post-receive.log
	- makes a tail option available on the push 
- a systemd service to restart systemd services when their service files change??
    