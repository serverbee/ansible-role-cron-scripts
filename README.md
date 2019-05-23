## Cron scripts role

This role use [ansible cron module](http://docs.ansible.com/ansible/latest/cron_module.html) for scheduling your scripts in user's crontab.
Also you can simply add your script with all it own content directly to group_vars or host_vars.

#### Variables

##### General

* `cron_scripts_dir`: [default: `/etc/scripts`]: Directory where will be store all cron scripts from this role

##### Cron sript content and crontab setting

* `cron_scripts_map`: [default: `{}`]: Cron script declarations
* `cron_scripts_map.key`: [required]: The identifier of the file (e.g. `first-example-script-name.sh:`)
* `cron_scripts_map.key.content`: [required]: Set the contents of the file directly in group_vars or host_vars
* `cron_scripts_map.key.arg`: [optional, default `null`]: Set additional argument(s) for cron sript
* `cron_scripts_map.key.user`: [optional, default `root`]: The specific user whose crontab should be modified
* `cron_scripts_map.key.minute`: [optional, default `*`]: Minute when the job should run (e.g. `0-59`, `*`, `*/2`, etc ) 
* `cron_scripts_map.key.hour`: [optional, default `*`]: Hour when the job should run (e.g. `0-23`, `*`, `*/2`, etc ) 
* `cron_scripts_map.key.day`: [optional, default `*`]: Day of the month the job should run (e.g. `1-31`, `*`, `*/2`, etc )
* `cron_scripts_map.key.month`: [optional, default `*`]: Month of the year the job should run (e.g. `1-12`, `*`, `*/2`, etc )
* `cron_scripts_map.key.weekday`: [optional, default `*`]: Day of the week that the job should run (e.g. `0-6` for Sunday-Saturday, `*`, etc )
* `cron_scripts_map.key.disabled`: [optional, default `no`]: If the job should be disabled (commented out) in the crontab

## Dependencies

None

#### Example(s)

##### Simple example

```yaml
---
- hosts: all
  roles:
    - cron-sripts 
  vars:
    cron_scripts_map:
      first-example-script-name.sh:
        content: |
          #!/bin/bash
          echo "Hello from cron!"
        minute: "0"
        hour: "1"
```

##### Full options example 

```yaml
---
- hosts: all
  roles:
    - cron-sripts 
  vars:
    cron_scripts_dir: /etc/example-scripts

    cron_scripts_map:
      second-example-script-name.sh:
        content: |
          #!/bin/bash
          echo "This script was launched at $(date '+%H:%M:%S on %D')"
        arg: "> /dev/null 2>&1"
        user: root
        minute: "5,10"
        hour: "*/2"
        day: "1-7"
        month: "1,6,12"
        weekday: "0,3"
```

#### License

GPLv3 license

#### Author Information

Vitaly Yakovenko
