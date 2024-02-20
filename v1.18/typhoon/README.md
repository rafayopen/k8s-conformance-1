# Typhoon

## Setup

Define a Typhoon Kubernetes v1.18.x cluster in a Terraform workspace. Pick any OS + platform combination marked [stable](https://github.com/poseidon/typhoon/blob/v1.18.0/README.md#modules) at the v1.18 release.

For example, a cluster on Google Cloud with Container Linux:

```
module "google-cloud-yavin" {
  source = "git::https://github.com/poseidon/typhoon//google-cloud/container-linux/kubernetes?ref=v1.18.0"

  # Google Cloud
  cluster_name  = "yavin"
  region        = "us-central1"
  dns_zone      = "example.com"
  dns_zone_name = "example-zone"

  # configuration
  ssh_authorized_key = "ssh-rsa AAAAB3Nz..."

  # optional
  worker_count       = 2
  enable_aggregation = "true"
}

# Obtain cluster kubeconfig
resource "local_file" "kubeconfig-yavin" {
  content  = module.yavin.kubeconfig-admin
  filename = "/home/user/.kube/configs/yavin-config"
}
```

Apply the declared cluster.

```
terraform init
terraform apply
```

To achieve complete conformance, you **must**:

* Enable aggregation with `enable_aggregation="true"`
* Allow inbound NodePort (30000-32767) traffic via firewall rules
* Not use Preemptible or Spot instances

Use the generated `kubeconfig`.

```
$ export KUBECONFIG=/home/user/.kube/configs/yavin-config
$ kubectl get nodes
NAME                                      STATUS ROLES   AGE VERSION
yavin-controller-0.c.example-com.internal Ready  <none>  6m  v1.18.0
yavin-worker-jrbf.c.example-com.internal  Ready  <none>  5m  v1.18.0
yavin-worker-mzdm.c.example-com.internal  Ready  <none>  5m  v1.18.0
```

## Reproduce Conformance Results

Use the `sonobuoy` command line tool (requires Go).

```
go get -u -v github.com/vmware-tanzu/sonobuoy
sonobuoy run
sonobuoy status
sonobuoy retrieve .
mkdir ./results; tar xzf *.tar.gz -C ./results
```

Inspect the results in `plugins/e2e/results/{e2e.log,junit.xml}`.
