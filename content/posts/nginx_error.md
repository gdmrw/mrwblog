---
title: Nginx pid error fix
date: 2022-10-21 10:50:32
tags: ["shell","nginx","linux"]
---
If you use `systemctl status nginx` to check nginx status you may find a pid error appear on status panel.  The words that appear may be :

```
Can't open PID file /run/nginx.pid (yet?) after start: Operation not permitted
Or
Can't open PID file /var/run/nginx.pid (yet?) after start: No such file or directory
```

This is becasue the pid file not generate before the nginx booted. 
The solution is to add following sentence into `/usr/lib/systemd/system/nginx.service`, it will let nginx wait 0.1s before executing the executable.

```ExecStartPost=/bin/sleep 0.1```

Add this sentence to the [service] part.

Rload and restart the nginx

```
systemctl daemon-reload
systemctl restart nginx
```

Problem fixed.