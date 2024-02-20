Harmonycloud Container Platform
An Enterprise Platform-as-a-Service based on Kubernetes

To Reproduce
Install the Harmonycloud product from here, the kubernetes version is v1.12.3.

The standard tool for running these tests is Sonobuoy. Sonobuoy is regularly built and kept up to date to execute against all currently supported versions of kubernetes.

Download the CLI by running:
$ go get -u -v github.com/heptio/sonobuoy
If you can't access http://www.gcr.io, you should download some pre-requisite images from other website. Then change 'imagePullPolicy' from "Always" to "IfNotPresent".

Deploy a Sonobuoy pod to your cluster with:

$ sonobuoy run
View actively running pods:
$ sonobuoy status 
To inspect the logs:
$ sonobuoy logs
Once sonobuoy status shows the run as completed, copy the output directory from the main Sonobuoy pod to a local directory:
$ sonobuoy retrieve .
This copies a single .tar.gz snapshot from the Sonobuoy pod into your local . directory. Extract the contents into ./results with:

mkdir ./results; tar xzf *.tar.gz -C ./results
NOTE: The two files required for submission are located in the tarball under plugins/e2e/results/{e2e.log,junit.xml}.

To clean up Kubernetes objects created by Sonobuoy, run:
sonobuoy delete