# MiaoYun

MiaoYun is a platform based on Docker container, supporting both Docker Swarm and Kubernetes container orchestration.

## How to Reproduce

First install MiaoYun v18.06.1. To install MiaoYun online, first get the online installation tool myctl, then run:
```
myctl deploy
```
Refer to the documentation for detailed description on installation parameters.

Then create a Kubernetes cluster and add nodes. Login to MiaoYun management platform, go to clusters page, create a new Kubernetes cluster, copy the add-node command and execute it on a node.

To setup kubectl, Copy the kubectl setup commands in settings and execute them on the remote node.

Run the conformance test:
Download a binary release of the sonobuoy v0.11.6, and run:
```
sonobuoy run
```

Wait for test success message and retrive the test results:
```
sonobuoy retrieve .
```



