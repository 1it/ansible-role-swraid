# Ansible Software RAID

Ansible role for manage partitions and the Software RAID arrays and optionally to mount the RAID devices. 

## Use this role at your own risk, you have to understand what are you doing.

## Variables
```yaml
partitions:
    - name: /dev/sdb
      volumes:
        - number: 1
          part_end: 1GiB
        - number: 5
          part_start: 1GiB
    - name: /dev/sdc
      volumes:
        - number: 1
          part_end: 1GiB
        - number: 5
          part_start: 1GiB

software_raid_alerts_email: "email@example.com"
software_raid_create_kwargs: "--run" # force the creation if there are any prompts

software_raid_devices:
- device: /dev/md2
  level: 1
  components:
    - /dev/sdb1
    - /dev/sdc1
  filesystem_type: "swap"
  mount_point: "none"
  mount_options: "sw"
  dump: 0
  passno: 0
- device: /dev/md3
  level: 1
  components:
    - /dev/sdb5
    - /dev/sdc5
  filesystem_type: "xfs"
  mount_point: "/mnt/backup"
  mount_options: "noatime,noexec,nodiratime"
  dump: 0
  passno: 0
```

## Testing

Test against vagrant. Add a yml file and environment variable in the 
make file to tell the Vagrantfile what yml config to run.

```
make test
```
