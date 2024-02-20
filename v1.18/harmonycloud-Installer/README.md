# Harmonycloud PaaS Container Platform Install 

Harmonycloud PaaS Container Platform Install is an Offline install Platform-as-a-Service platform based on Kubernetes

## To Reproduce

Install Harmonycloud Container Platform v2.8.0. the kubernetes version is v1.18.0.

 * install Harmonycloud Container Platform one master and two nodes for Kubernetes cluster. Centos is recommended.

 * Packages: 

   1. sealos
   
   2. kube1.18.0.tar.gz


### Installation process:

1. Download and install sealos

```
$ wget -c https://sealyun.oss-cn-beijing.aliyuncs.com/latest/sealos && \
    chmod +x sealos && mv sealos /usr/bin
```

2. Download the offline resource pack

```
$ wget -c https://sealyun.oss-cn-beijing.aliyuncs.com/d551b0b9e67e0416d0f9dce870a16665-1.18.0/kube1.18.0.tar.gz 

```
3. Install Platform and kubernetes cluster

```
$ sealos init --passwd 123456 \
	--master 192.168.0.2  --node 192.168.0.3  --node 192.168.0.4  \
	--pkg-url /root/kube1.18.0.tar.gz \
	--version v1.18.0

```
### Run Sonobouy

The standard tool for running these tests is [Sonobuoy](https://github.com/heptio/sonobuoy). Sonobuoy is regularly built and kept up to date to execute against all currently supported versions of kubernetes.

1. Download the CLI by running:

```
$ tar -xzvf sonobuoy_0.18.0_linux_amd64 .tar.gz
$ mv sonobuoy /usr/bin/
```

2. If you can't access [http://www.gcr.io](http://www.gcr.io/), you should download some pre-requisite images from other website. Then change 'imagePullPolicy' from "Always" to "IfNotPresent".

3. Deploy a Sonobuoy pod to your cluster with:

```
$ sonobuoy run --mode=certified-conformance
```

4. View actively running pods:

```
$ sonobuoy status 
```

5. To inspect the logs:

```
$ sonobuoy logs
```

6. Once `sonobuoy status` shows the run as `completed`, copy the output directory from the main Sonobuoy pod to a local directory:

```
$ outfile=$(sonobuoy retrieve)
```

This copies a single `.tar.gz` snapshot from the Sonobuoy pod into your local
`.` directory. Extract the contents into `./results` with:

```
mkdir ./results; tar xzf $outfile -C ./results
```

**NOTE:** The two files required for submission are located in the tarball under **plugins/e2e/results/{e2e.log,junit.xml}**. 

7. To clean up Kubernetes objects created by Sonobuoy, run:

```
sonobuoy delete
```
