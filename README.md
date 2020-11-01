Cluster Manipulation Scripts
================================

This repository contains a set of Ansible playbooks to perform common cluster management tasks.

    ansible_deploy
    ├── distr
    ├── files
    ├── include
    ├── logs
    ├── playbooks
    ├── config.yml
    └── development


Put relevant Debian package files into `distr/` directory:

```
    distr
    └── mc_4.8.18-1_amd64.deb
```

Put j2-conf files into `files/` directory:

```
    files
    ├── nginx.conf.j2
    └── ntp.conf.j2
```

The `include/` directory for vars which may be use in playbooks:

```
    include
    └── vars.yml
```

The `logs/` directory for logs which fetched from hosts:

The `playbooks/` directory for playbook instructions which will be run on each server :

```
    playbooks/
    ├── copy-logs-from-servers.yml
    ├── mc-deb-install.yml
    ├── mount-storage.yml
    ├── nginx-install.yml
    ├── ntp-install.yml
    ├── reboot.yml
    ├── remove_files.yml
    ├── replace-txt.yml
    ├── service.yml
    └── uri.yml
```


Install or Update MC
-----------------------

Put relevant Debian package files into `distr/` directory:

```
    distr
    └── mc_4.8.18-1_amd64.deb
```

Update and commit `./config.yml` file:

```
    mc_version: '4.1.1.7637'
```

Run `mc-deb-install` playbook:

    ansible-playbook -v -i development playbooks/mc-deb-install.yml

To limit the range of nodes to which playbook applies use `--limit` option:

    ansible-playbook -v -i development playbooks/mc-deb-install.yml --limit "host[1:3]"


Install or Update NTP
-----------------------

Install ntp via apt. Run `ntp-install` playbook:

    ansible-playbook -v -i development playbooks/ntp-install.yml

To limit the range of nodes to which playbook applies use `--limit` option:

    ansible-playbook -v -i development playbooks/ntp-install --limit "host[1:3]"


Collect Logs
------------------

To collect Logs use `copy-logs-from-servers` playbook:

    ansible-playbook -v -i development playbooks/copy-logs-from-servers.yml

Logs will be downloaded into `./logs` directory, separate file for each node:

```
    logs
    ├── 20200927T130808_host1_logs.tar.xz
    ├── 20200927T130808_host2_logs.tar.xz
    └── 20200927T131141_host3_logs.tar.xz

```

**NOTE**: if no `--limit` is used logs will be collected from the entire cluster, which can be very time consuming.



Other
-----

Check out other available playbooks in `./playbooks` directory to what else is available.

