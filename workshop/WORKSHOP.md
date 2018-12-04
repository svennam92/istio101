# Beyond the Basics: Istio and IBM Cloud Kubernetes Service
[Istio](https://www.ibm.com/cloud/info/istio) is an open platform to connect, secure, and manage a network of microservices, also known as a service mesh, on cloud platforms such as Kubernetes in IBM Cloud Kubernetes Service. With Istio, You can manage network traffic, load balance across microservices, enforce access policies, verify service identity on the service mesh, and more.

In this course, you can see how to install Istio alongside microservices for a simple mock app called Guestbook. When you deploy Guestbook's microservices into an IBM Cloud Kubernetes Service cluster where Istio is installed, you inject the Istio Envoy sidecar proxies in the pods of each microservice.

## Objectives
After you complete this course, you'll be able to:
- Download and install Istio in your cluster
- Deploy the Guestbook sample app
- Use metrics, logging and tracing to observe services
- Set up the Istio Ingress Gateway
- Perform simple traffic management, such as A/B tests and canary deployments
- Secure your service mesh
- Enforce policies for your microservices

## Get Started
In this section, you will create your own IBM Cloud account, and then get access to a IBM Cloud Lab account which contains pre-provisioned clusters.

1. Create your own [IBM Cloud account](https://cloud.ibm.com).
2. Go to [Get Cluster](http://get-cluster.mybluemix.net) and enter your IBM ID (the email you used to sign up) and the lab key `istiorocks`.
3. Refresh your [IBM Cloud Dashboard](https://cloud.ibm.com) and click on the account selection drop down.
4. Select **IBM**
5. Click on **View all** in the Resource Summary tile
6. Under **Kubernetes Clusters**, click on the cluster that has been assigned to you.

You will use this cluster for this lab.

## Workshop setup
You will perform the following exercises in the lab.

- [Exercise 1 - Accessing a Kubernetes cluster with IBM Cloud Kubernetes Service](exercise-1/README.md)
- [Exercise 2 - Installing Istio](exercise-2/README.md)
- [Exercise 3 - Deploying Guestbook with Istio Proxy](exercise-3/README.md)

## Creating a service mesh with Istio

- [Exercise 4 - Observe service telemetry: metrics and tracing](exercise-4/README.md)
- [Exercise 5 - Expose the service mesh with the Istio Ingress Gateway](exercise-5/README.md)
- [Exercise 6 - Perform traffic management](exercise-6/README.md)
- [Exercise 7 - Secure your service mesh](exercise-7/README.md)
- [Exercise 8 - Enforce policies for microservices](exercise-8/README.md)

## Cleaning up the Workshop

We have a script that will remove [ibmcloud](https://console.bluemix.net/docs/cli/index.html#overview) at [here](cleanup/clean_your_local_machine.sh) and unset your `KUBECONFIG` for you.

We have given you a [script](cleanup/clean_your_k8s_cluster.sh) as a conveant way to remove Istio and the guestbook
application from your instance.

**NOTE**: This puts your kubernetes cluster in a empty state, so do not run this on anything other then
a place you are willing to loose everything.
