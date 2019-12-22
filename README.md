# mikroways.m7s-k8s-backups

Backup etcd nodes and kubernetes master nodes. It uses kubespray groups, but
this can be customized with role variables.

## Role Variables

* `m7s_k8s_backups_state:` whether backups are enabled or not. By default are
  enabled.
* `m7s_k8s_backups_destination:` where backups will be stored. By default `/var/lib/m7s-k8s-backups`.
* `m7s_k8s_backups_master_schedule:` frequency of master backups. Once a day at
  3 am is default value. This variable must use crontab format like `0 3 * * *`.
* `m7s_k8s_backups_etcd_minute_schedule:` frequency of etcd backups. By default
  is every 30 minutes: `*/30`.
* `m7s_k8s_backups_etcd_keys_special_time_schedule:` frequency of etcd
  certificates backups. By default is `daily`.
* `m7s_k8s_backups_date_format:` filename trailing date format. By default `%Y-%m-%d_%H-%M-%S_%Z`
* `m7s_k8s_backups_retain:` retention in days. By default 5 days of retention.
* `m7s_k8s_backups_etcd_env_path:` source script with custom environment set by
  kubespray. Defaults to `/etc/etcd.env`.
* `m7s_k8s_backups_directory_on_master:` directory to backup from master nodes.
  Defaults to `/etc/kubernetes`.
* `m7s_k8s_backups_directory_on_etcd:` directory to backup from etcd noes.
  Defaults to `/etc/ssl/etcd/ssl`
* `m7s_k8s_backups_ansible_k8s_master_group:` ansible group of master nodes.
  Defaults to `kube-maste`
* `m7s_k8s_backups_ansible_k8s_etcd_group:` ansible group of etcd nodes.
  Defaults to `etcd`.


## Example Playbook

```yaml
- hosts: kube-master:etcd
  roles:
    - { role: mikroways.m7s-k8s-backups, tags: [ backups ] }

```

This example allows to test backup role runing:

```
ansible-playbook -t backups all your-playbook.yml
```


## License

GPLv2

