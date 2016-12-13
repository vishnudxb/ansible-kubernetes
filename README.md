#Deploy a production ready kubernetes cluster

- **High available** cluster (AWS)
- **Composable** (Choice of the network plugin for instance)
- Support most popular **Linux distributions**
- **Continuous integration tests**


```

To deploy the cluster:
1. Update inventory/hosts file with actual IP's
2. Run:  ansible-playbook kube-cluster.yml -i inventory/hosts -vvvv

```

Supported Linux distributions
===============

* **CoreOS**
* **Debian** Wheezy, Jessie
* **Ubuntu** 14.10, 15.04, 15.10, 16.04
* **Fedora** 23
* **CentOS/RHEL** 7

Versions
--------------

[kubernetes](https://github.com/kubernetes/kubernetes/releases) v1.4.6 <br>
[etcd](https://github.com/coreos/etcd/releases) v3.0.6 <br>
[flanneld](https://github.com/coreos/flannel/releases) v0.6.2 <br>
[calicoctl](https://github.com/projectcalico/calico-docker/releases) v0.22.0 <br>
[weave](http://weave.works/) v1.6.1 <br>
[docker](https://www.docker.com/) v1.10.3 <br>


Requirements
--------------

* The target servers must have **access to the Internet** in order to pull docker images.
* The **firewalls are not managed**, you'll need to implement your own rules the way you used to.
in order to avoid any issue during deployment you should disable your firewall
* **Copy your ssh keys** to all the servers part of your inventory.
* **Ansible v2.x and python-netaddr**


## Network plugins
You can choose between 3 network plugins. (default: `flannel` with vxlan backend)

* [**flannel**](https://github.com/coreos/flannel/): gre/vxlan (layer 2) networking.

* [**calico**](https://github.com/projectcalico/calico-docker): bgp (layer 3) networking.

* [**weave**](https://www.weave.works/): Weave is a lightweight container overlay network that doesn't require an external K/V database cluster. <br>
(Please refer to `weave` [troubleshooting documentation](http://docs.weave.works/weave/latest_release/troubleshooting.html))

The choice is defined with the variable `kube_network_plugin`
