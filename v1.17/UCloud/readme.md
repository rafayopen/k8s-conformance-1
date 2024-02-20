### How to Reproduce:

#### Before start:

You must register a UCLoud Cloud Account following [this](https://passport.ucloud.cn/#register).

#### Create UK8S Cluster

After login in UCLoud Console，You can Create a UK8S Cluster in Hong Kong region in this [pages](https://console.ucloud.cn/uk8s/manage). The Kubernetes Version is v1.17.4 bydefault.

1. step one : Click "Create Cluster" Button ;

2. step two : Config Master and Node, or you can just use the default config;

3. step three: Set password for the node of  cluster;

4. step four: Click "Purchase Now" button, the k8s cluster will running about  ten minutes later;

#### Access Cluster

The Nodes can't access from internet until bind a EIP to vm. You can bind EIP to any nodes in [uhost page](https://console.ucloud.cn/uhost/uhost).

After did that, you can ssh to the node or master.

#### Run Conformance Test

Run command as below:

```
# install golang first.

go get -u -v github.com/heptio/sonobuoy

sonobuoy run

sonobuoy status

sonobuoy logs

```
Wait for abount 2 hours for the test to be finished.once sonobuoy status shows the run as completed to indicate that the test has been finished, then run the following command to extract the test results.

```
sonobuoy retrieve .

mkdir ./results; tar xzf *.tar.gz -C ./results

```
