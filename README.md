# etcd-ansible

Ansible playbooks for deploying etcd cluster(with TLS).

## Getting started

[etcd clustering guide](https://etcd.io/docs/v3.4.0/op-guide/clustering/)

- enable_tls `True/False`
- Add etcd node to group in hosts

    ```ini
    [etcd]
    <etcd_node1>
    <etcd_node2>
    <etcd_node3>
    ```

### Deploy with Ansible

```bash
$ ansible-playbook -i hosts ./deploy.yaml
```

### Check cluster health

- with TLS

    ```bash
    $ ETCDCTL_API=3 etcdctl --endpoints=https://etcd1:2379,https://etcd2:2379,https://etcd3:2379 \
        --cacert=/etc/etcd/pki/ca.pem \
        --cert=/etc/etcd/pki/etcd-client.pem \
        --key=/etc/etcd/pki/etcd-client-key.pem \
        endpoint health
    https://etcd1:2379 is healthy: successfully committed proposal: took = 10.233885ms
    https://etcd3:2379 is healthy: successfully committed proposal: took = 10.83476ms
    https://etcd2:2379 is healthy: successfully committed proposal: took = 10.603532ms
    ```

- without TLS

    ```bash
    $ ETCDCTL_API=3 etcdctl --endpoints=http://etcd1:2379,http://etcd2:2379,http://etcd3:2379 \
        endpoint health
    http://etcd1:2379 is healthy: successfully committed proposal: took = 3.326095ms
    http://etcd2:2379 is healthy: successfully committed proposal: took = 2.748218ms
    http://etcd3:2379 is healthy: successfully committed proposal: took = 2.487955ms
    ```
