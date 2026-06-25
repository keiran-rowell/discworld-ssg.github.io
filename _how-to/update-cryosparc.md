---
title: "Updating CryoSPARC"
author: nathan_glades 
---

### Introduction

As you may know, Discworld operates per-user CryoSPARC installations. This means that you have your own CryoSPARC server that is not shared with anyone else. This has the benefit that you are able to choose when and to what version you would like your CryoSPARC instance to run.

### Upgrading CryoSPARC

If you see that an update is available, and you would like to update, follow the below steps:

Firstly, close any currently running CryoSPARC sessions. This can be done via the web-portal by clicking the “X” button next to the “Connect” button.


![CryoSPARC portal connection]({{ site.url }}{{ site.baseurl }}/assets/images/cryosparc-connection-stopped.png)

Then, connect to Discworld via the login node, and start an interactive session with a GPU. To avoid interruptions due to network connection failures, it is recommended to perform an update within a [Tmux session](/how-to/using-tmux).

```bash
ssh z3141592@discworld.analytical.unsw.edu.au
[z3141592@discworld0 ~]$ sinteractive --gpu
[z3141592@c01 ~]$
```

Next, run the “update” command on the CryoSPARC master server. CryoSPARC should automatically start updating.

```bash
[z3141592@c01 ~]$ ~/.local/usr/opt/cryosparc/cryosparc_master/bin/cryosparcm update
─────────────────────────────────────────────────────────────────────────────────────
Checking for update...
    current version: v5.0.0
     latest version: v5.0.1
Update available!
```

As CryoSPARC runs on a SLURM cluster, CryoSPARC will not automatically update it’s worker. This is done as a precaution to prevent the worker from being updated if jobs are still running. In our instance, we can be reasonably confident that no CryoSPARC jobs will be running. Within the same session, run the following commands to update the worker:

```bash
[z3141592@c01 ~]$ cp ~/.local/usr/opt/cryosparc/cryosparc_master/cryosparc_worker.tar.gz ~/.local/usr/opt/cryosparc/cryosparc_worker/
[z3141592@c01 ~]$ ~/.local/usr/opt/cryosparc/cryosparc_worker/bin/cryosparcw update
─────────────────────────────────────────────────────────────────────────────────────
Updating worker at /home/z3545907/.local/usr/opt/cryosparc/cryosparc_worker
─────────────────────────────────────────────────────────────────────────────────────
Checking versions...
    current worker version: v5.0.0
    new worker version:     v5.0.1
Deleting old files...
Extracting...
```

Finally, and most important, **you will need to manually stop CryoSPARC**. For whatever reason, updating CryoSPARC causes it to start once the update is completed. This will cause frustrating behaviour when you attempt to start CryoSPARC again via the portal. Please run the following commands to stop CryoSPARC:

```bash
[z3141592@c01 ~]$ ~/.local/usr/opt/cryosparc/cryosparc_master/bin/cryosparcm stop
Stopping CryoSPARC ...
app: stopped
app_api: stopped
cache: stopped
api:0: stopped
api:1: stopped
api:2: stopped
command_vis: stopped
scheduler: stopped
database: stopped
Shut down
```

The update is now complete. You may start CryoSPARC via the web portal.

![CryoSPARC update completion alert]({{ site.url }}{{ site.baseurl }}/assets/images/cryosparc_updated.png)

### Troubleshooting
#### CryoSPARC is taking a while to start
After updating CryoSPARC, it can take some time to start the database the first time. Please allow CryoSPARC some extra time to start the service. If the service has not started after 5 minutes, please see [these troubleshooting steps](). As always, feel free to reach out if you need assistance.
