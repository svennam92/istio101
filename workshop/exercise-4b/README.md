# Exercise 4 - Logging and Monitoring

## Using IBM Log Analysis with LogDNA

IBM Log Analysis with LogDNA is a third-party service that you can include as part of your IBM Cloud architecture to add log management capabilities. IBM Log Analysis with LogDNA is operated by LogDNA in partnership with IBM.

The service plan that you choose for an IBM Log Analysis with LogDNA instance defines the number of days that data is stored and retained in LogDNA. For example, if you choose the Free plan, data is not stored at all. However, if you choose the 7 day plan, data is stored for 7 days and you have access to it through the LogDNA Web UI.

## Configure your cluster with LogDNA

1. Switch to your personal IBM Cloud account.
1. Create an instance of [IBM Log Analysis with LogDNA](https://cloud.ibm.com/observe/logging/create) from the catalog:
   1. Set the **Service name** to **YOUR_IBM_ID-logdna**.
   1. Select the location where your cluster is created. If the location is not in the list, pick Dallas (us-south).
   1. Use the default resource group.
   1. Click **Create**.
1. In the [**Observability** category, under Logging](https://cloud.ibm.com/observe/logging), locate the service instance you created.
1. Click **Edit log sources**:
   1. Select **Kubernetes** as a source
   1. Run the listed commands against your Kubernetes cluster.

## View logs in the LogDNA dashboard

1. Click **View LogDNA** to open the LogDNA console
1. Use `namespace:<namespace name>` to view only the logs of the applications deployed to the specified namespace, such as `namespace:default`
1. As you go through the next steps, keep an eye on the LogDNA console for new log statements coming from your apps deployed in this namespace.

![LogDNA dashboard](./images/observability-logging-logdna.png)

{% hint style='tip' %}
Find more about IBM Log Analysis with LogDNA in the [IBM Cloud documentation](https://cloud.ibm.com/docs/services/Log-Analysis-with-LogDNA/index.html#getting-started).
{% endhint %}

## Using IBM Cloud Monitoring with Sysdig

Sysdig monitor is a third-party cloud-native container-intelligence management system. You can use this to gain operational visibility for your applications, services, and platform. Sysdig offers administrators, DevOps teams and developers advanced features to monitor and troubleshoot, define alerts, and design custom views.

![Sysdig in catalog](./images/observability-monitoring-sysdig-catalog.png)

## Create a Sysdig service instance

1. Switch to your personal IBM Cloud account.
2. Create an instance of [IBM Cloud Monitoring with Sysdig](https://cloud.ibm.com/observe/monitoring/create) from the catalog:
   1. Set the **Service name** to **YOUR_IBM_ID-sysdig**.
   2. Select the location where your cluster is created. If the location is not in the list, pick Dallas (us-south).
   3. Use the default resource group.
   4. Click **Create**.
3. In the [**Observability** category, under Monitoring](https://cloud.ibm.com/observe/monitoring), locate the service instance you created.
4. Click **View access keys** and copy your access key as it will be needed in later steps.


## Configure your cluster with Sysdig

1. On IBM Cloud Dashboard, click on Catalog. 

2. Search for SysDig and create an instance using the Trial plan.

3. Follow the instructions on the Sysdig dashboard to configure your cluster.

## View metrics with Sysdig

1. Click **View Sysdig** to open the Sysdig console
2. In the Sysdig _Welcome_ wizard
   1. Select **Kubernetes** as the installation method.
   2. It should show one or more agents already connected.
   3. Select **GO TO NEXT STEP**.
   4. And finally **LET'S GET STARTED**
3. Navigate the Sysdig console to get metrics on your Kubernetes cluster, nodes, deployments, pods, containers.
   1. Under **Explore**, select **Containerized Apps** to view raw metrics for all workloads running on the cluster.
   2. Under **Dashboard**, select **My Shared Dashboards / HTTP Overview** to get a global view of the cluster HTTP load.
   3. Under **Dashboard**, select **My Shared Dashboards / Overview by Host** to understand how nodes are currently performing.

   {% hint style='info' %}
   If Kubernetes-specific views do not show data, wait till your cluster starts sending metrics to Sysdig and refresh the Sysdig monitor console.
   {% endhint %}

![Sysdig dashboard](./images/observability-monitoring-sysdig.png)

{% hint style='tip' %}
Find more about IBM Cloud Monitoring with Sysdig in the [IBM Cloud documentation](https://cloud.ibm.com/docs/services/Monitoring-with-Sysdig/index.html#getting-started).
{% endhint %}