# Exercise 1 - Accessing your Kubernetes Cluster

You must already have an IBM account, with a cluster created or assigned to you as documented in [previous step](../GETSTARTED.md).

## Start your local sandbox environment
A docker container with the required tools for this lab is provided for you. Use this container as your local terminal. It exposes a few ports for use with web applications. If you do NOT want to use this container, you can directly [download](https://console.bluemix.net/docs/cli/reference/ibmcloud/download_cli.html) the `ibmcloud` cli to your laptop.

1. Download and install [Docker](https://www.docker.com/get-started) if you don't already have one.
2. Start the container 
```
docker run -it -p 8080-8085:8080-8085 jjasghar/ibm-cloud-cli
```
3. Log in to IBM Cloud: `ibmcloud login`
4. Choose `us-south` and the `IBM` account

## Access your cluster
Learn how to set the context to work with your cluster by using the `kubectl` CLI, access the Kubernetes dashboard, and gather basic information about your cluster.

1.  Set the context for your cluster in your CLI. Every time you log in to the IBM Cloud Kubernetes Service CLI to work with the cluster, you must run these commands to set the path to the cluster's configuration file as a session variable. The Kubernetes CLI uses this variable to find a local configuration file and certificates that are necessary to connect with the cluster in IBM Cloud.

    a. List the available clusters.

    ```shell
    ibmcloud ks clusters
    ```

    b. Download the configuration file and certificates for your cluster using the `cluster-config` command.

    ```shell
    ibmcloud ks cluster-config <your_cluster_name>
    ```

    c. Copy and paste the output export command from the previous step to set the `KUBECONFIG` environment variable and configure your CLI to run `kubectl` commands against your cluster. Example:
    `export KUBECONFIG=/Users...`

2.  Get basic information about your cluster and its worker nodes. This information can help you manage your cluster and troubleshoot issues.

    a.  View details of your cluster.

    ```shell
    ibmcloud ks cluster-get <your_cluster_name>
    ```

    b.  Verify the worker nodes in the cluster.

    ```shell
    ibmcloud ks workers <your_cluster_name>
    ibmcloud ks worker-get <worker_ID>
    ```

3.  Validate access to your cluster.

    a.  View nodes in the cluster.

    ```shell
    kubectl get node
    ```

    b.  View services, deployments, and pods.

    ```shell
    kubectl get svc,deploy,po --all-namespaces
    ```

## Clone the lab repo

1. From your command line, run:

    ```shell
    git clone https://github.com/IBM/istio101
    cd istio101/workshop
    ```

    This is the working directory for the workshop. You will use the example `.yaml` files that are located in the `workshop/plans` directory in the following exercises.

### [Continue to Exercise 2 - Installing Istio](../exercise-2/README.md)
