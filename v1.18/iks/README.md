# IBM Cloud Kubernetes Service

You'll first need to get started with IBM Cloud Kubernetes Service by setting up
an IBM Cloud account. For details, see the
[getting started](https://cloud.ibm.com/docs/containers?topic=containers-getting-started)
instructions. Then follow the steps below to create a cluster and run the conformance tests.

## Create a cluster

If you haven't already done so,
[install the IBM Cloud CLI and plugins](https://cloud.ibm.com/docs/containers?topic=containers-cs_cli_install#cs_cli_install_steps)
for IBM Cloud Kubernetes Service. You may then create a cluster using the CLI or UI.

### CLI

```
$ # Option 1: Create a cluster on classic infrastructure.
$ ibmcloud ks cluster create classic --name conformance --version 1.18 --zone ZONE --flavor FLAVOR --private-vlan VLAN --public-vlan VLAN --workers COUNT

$ # Option 2: Create a Virtual Private Cloud (VPC) cluster with worker nodes on Generation 1 infrastructure.
$ ibmcloud ks cluster create vpc-classic --name conformance --version 1.18 --zone ZONE --flavor FLAVOR --vpc-id ID --subnet-id ID --workers COUNT
```

### UI

Go to [IBM Cloud catalog](https://cloud.ibm.com/catalog?category=containers)
and select `Kubernetes Service` and follow the instructions to create a cluster.

## Run conformance tests

Wait for the cluster and all worker nodes to reach `normal` state.

```
$ ibmcloud ks cluster config --admin --cluster conformance
$ ibmcloud ks cluster get --cluster conformance
$ ibmcloud ks workers --cluster conformance
```

Then follow the
[test instructions](https://github.com/cncf/k8s-conformance/blob/master/instructions.md#running)
to run the conformance tests.
