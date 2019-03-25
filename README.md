# ansible-etcds

Here is a project for deploying etcds to 3 nodes.

## Getting started

[etcd clustering guide](https://coreos.com/etcd/docs/latest/v2/clustering.html)

Add an etcds group to /etc/ansible/hosts

```
[etcds]
<master_ip1>
<master_ip2>
<master_ip3>
```


### Deploying

* **Replace master_ips in /group_vars.all**
* `$ ansible-playbook ./deploy.yml`
