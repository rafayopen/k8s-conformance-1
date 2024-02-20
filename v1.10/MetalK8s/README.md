# MetalK8s
Official documentation:
 - https://metal-k8s.readthedocs.io

# Reproduce Conformance Results:

## Pre-Reqs
- An OpenStack cluster
- The official CentOS 7.4 1711 image pre-loaded in Glance
- 5 VMs with 8 vCPUs, 16GB of RAM, 40GB of local storage
- 5 250GB Cinder volumes

## Provision
- Create the 5 VM instances using the CentOS 7.4 image, and attach a Cinder
  volume to each of them, which becomes `/dev/vdb`.

- Populate an Ansible inventory (e.g. in `~/inventory/metalk8s.ini`) according
  to your deployment:

```
kube-server-1 ansible_host=10.5.0.1 ansible_user=centos ansible_become=True ansible_become_method=sudo
kube-server-0 ansible_host=10.4.0.2 ansible_user=centos ansible_become=True ansible_become_method=sudo
kube-server-3 ansible_host=10.3.0.3 ansible_user=centos ansible_become=True ansible_become_method=sudo
kube-server-2 ansible_host=10.2.0.4 ansible_user=centos ansible_become=True ansible_become_method=sudo
kube-server-4 ansible_host=10.1.0.5 ansible_user=centos ansible_become=True ansible_become_method=sudo

[etcd]
kube-server-1
kube-server-0
kube-server-3

[kube-master]
kube-server-0
kube-server-3

[kube-node]
kube-server-1
kube-server-0
kube-server-3
kube-server-2
kube-server-4

[k8s-cluster:children]
kube-master
kube-node

[k8s-cluster:vars]
metal_k8s_lvm={'vgs': {'kubevg': {'drives': ['/dev/vdb']}}}
```

- Ensure the VMs are accessible using key-based SSH. If required, launch
  `ssh-agent` and add your private key:

```
$ source <(ssh-agent)
$ ssh-add
```

The remaining steps are outlined in the [MetalK8s Quickstart
Guide](https://metal-k8s.readthedocs.io/en/latest/usage/quickstart.html)

```
$ curl -LO https://github.com/scality/metal-k8s/archive/0.1.0.tar.gz
$ tar xf 0.1.0.tar.gz
$ cd metal-k8s-0.1.0
$ make shell
Launching MetalK8s shell environment. Run 'exit' to quit.
(metal-k8s)$ ansible-playbook -i ~/inventory/metalk8s.ini playbooks/deploy.yml
(metal-k8s)$ export KUBECONFIG=~/inventory/artifacts/admin.conf
```

## Running Sonobuoy and Collecting Results

Follow the [instructions](
https://github.com/scality/k8s-conformance/blob/master/instructions.md) as found
in the [CNCF K8s Conformance repository](
https://github.com/cncf/k8s-conformance):

```
(metal-k8s)$ curl -L https://raw.githubusercontent.com/cncf/k8s-conformance/master/sonobuoy-conformance.yaml | kubectl apply -f -
...
```
