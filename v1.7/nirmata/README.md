
To reproduce the test results, follow the steps to create a new Kubernetes cluster from scratch using Nirmata:

1. On board your cloud resources to Nirmata using Direct Connect or by creating a cloud provider host group
2. Once all the hosts are connected, go to the Clusters panel and click on the Add Cluster button to launch the wizard
2. Select Kubernetes as the Container Orchestrator and on the next page select: No - Install and manage Kubernetes for me
3. Provide the cluster name and add host groups that you would like to install the cluster on. Also select the master nodes. Click on "Create cluster and start the installation" button to proceed with the cluster install.
4. Within a few minutes, the cluster will be deployed, the Nirmata controller should connect and the cluster state will show as Connected. 
5. Once the cluster is deployed and in Ready state, you can run the conformance tests using kubectl:

`curl -L https://raw.githubusercontent.com/cncf/k8s-conformance/master/sonobuoy-conformance.yaml | kubectl apply -f -`
