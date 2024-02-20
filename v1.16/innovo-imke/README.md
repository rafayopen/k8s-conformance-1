To create the cluster: 

Step 1

You will need an account for our OpenStack platform Optimist and our Kubernetes platform IMKE. The credentials will be used for both
https://dashboard.optimist.innovo.cloud/
and 
https://imke.cloud

Please email sales@innovo-cloud.de and ask for a new account credentials for Optimist and IMKE to be used by Cloud Native Computing Foundation (CNCF) Conformance tests for v1.16/innovo-imke 

Follow the steps in the email you recieve and login and change the password. Once this has been done then you should be able to login to https://imke.cloud


```
1. Login to https://imke.cloud
2. Create a new project
3. Create a new cluster in the project and select kubernetes version 1.16.3
4. Choose the OpenStack as the Provider
5. Choose a Datacenter location
6. Enter your Provider Credentials and create a 3 nodes node group with Container Linux as distribution and the m1.medium as the flavor
7. Check the requested settings and press Create Cluster
8. Wait for the cluster to be ready

```
https://docs.imke.cloud/en/guides/


Once the cluster is up and running you can download the kubeconfig details by following these instructions

https://imke.cloud/projects/<project id>/clusters

then select the cluster and then click the download button

https://docs.imke.cloud/en/guides/connectingtoacluster/

You will eventually get a download a file called kubeconfig-admin-<CLUSTERID>

and you will be able to set KUBECONFIG

```
export KUBECONFIG=$(pwd)/kubeconfig-admin-<CLUSTERID>
```

If you have any issues please email support@innovo-cloud.de 

