# Exercise 2 - Installing Istio on IBM Cloud Kubernetes Service

In this module, you will download the Istio installation files and then deploy it to your cluster.

1. Download the `istioctl` client:

    ```shell
    curl -L https://git.io/getLatestIstio | sh -
    ```

2. Add the `istioctl` client to your PATH by copying and pasting the `export PATH=` line in the output of the previous command. Your command will look something like `export PATH="$PATH:/h...`

3. Change the directory to the Istio installation files location.	

     ```shell	
    cd istio-1.0.6	
    ```	

4. Install Istio’s Custom Resource Definitions via kubectl apply, and wait a few seconds for the CRDs to be committed in the kube-apiserver:	

     ```shell	
    kubectl apply -f $PWD/install/kubernetes/helm/istio/templates/crds.yaml	
    ```	

5. Now let's deploy Istio into the `istio-system` namespace in your Kubernetes cluster:	

     ```shell	
    kubectl apply -f $PWD/install/kubernetes/istio-demo.yaml	
    ```
6. Ensure that the `istio-*` Kubernetes services are deployed before you continue.

    ```shell
    kubectl get svc -n istio-system
    ```

    ```shell
    NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                                                                                                                   AGE
    grafana                  ClusterIP      172.21.76.33     <none>         3000/TCP                                                                                                                  105s
    istio-citadel            ClusterIP      172.21.162.98    <none>         8060/TCP,9093/TCP                                                                                                         27m
    istio-egressgateway      ClusterIP      172.21.21.166    <none>         80/TCP,443/TCP                                                                                                            27m
    istio-galley             ClusterIP      172.21.13.60     <none>         443/TCP,9093/TCP                                                                                                          27m
    istio-ingressgateway     LoadBalancer   172.21.240.46    169.62.47.34   80:31380/TCP,443:31390/TCP,31400:31400/TCP,15011:32142/TCP,8060:32609/TCP,853:31738/TCP,15030:32413/TCP,15031:30916/TCP   27m
    istio-pilot              ClusterIP      172.21.93.10     <none>         15010/TCP,15011/TCP,8080/TCP,9093/TCP                                                                                     27m
    istio-policy             ClusterIP      172.21.2.51      <none>         9091/TCP,15004/TCP,9093/TCP                                                                                               27m
    istio-sidecar-injector   ClusterIP      172.21.205.142   <none>         443/TCP                                                                                                                   27m
    istio-telemetry          ClusterIP      172.21.8.65      <none>         9091/TCP,15004/TCP,9093/TCP,42422/TCP                                                                                     27m
    jaeger-agent             ClusterIP      None             <none>         5775/UDP,6831/UDP,6832/UDP                                                                                                105s
    jaeger-collector         ClusterIP      172.21.57.199    <none>         14267/TCP,14268/TCP                                                                                                       105s
    jaeger-query             ClusterIP      172.21.44.156    <none>         16686/TCP                                                                                                                 105s
    kiali                    ClusterIP      172.21.24.237    <none>         20001/TCP                                                                                                                 105s
    prometheus               ClusterIP      172.21.55.217    <none>         9090/TCP                                                                                                                  27m
    tracing                  ClusterIP      172.21.152.148   <none>         80/TCP                                                                                                                    105s
    zipkin                   ClusterIP      172.21.96.122    <none>         9411/TCP                                                                                                                  104s
    ```

7. Ensure the corresponding pods `istio-citadel-*`, `istio-ingressgateway-*`, `istio-pilot-*`, and `istio-policy-*` are all in **`Running`** state before you continue.

    ```shell
    kubectl get pods -n istio-system
    ```

    ```shell
    grafana-76dcdfc987-f522b                  1/1     Running   0          4m32s
    istio-citadel-869c7f9498-zpjk5            1/1     Running   0          29m
    istio-egressgateway-69bb5d4585-lkzfq      1/1     Running   0          29m
    istio-galley-75d7b5bdb9-gjz4k             1/1     Running   0          29m
    istio-ingressgateway-5c8764db74-bz4cp     1/1     Running   0          29m
    istio-pilot-55fd7d886f-zzqhf              2/2     Running   0          29m
    istio-policy-6bb6f6ddb9-5xcts             2/2     Running   0          29m
    istio-sidecar-injector-7d9845dbb7-8gd6x   1/1     Running   0          29m
    istio-telemetry-7695b4c4d4-4vlvq          2/2     Running   0          29m
    istio-tracing-55bbf55878-6bd82            1/1     Running   0          4m32s
    kiali-7d95477bfc-jrgng                    1/1     Running   0          4m32s
    prometheus-5d5cb44877-bf66g               1/1     Running   0          29m
    ```

    Before you continue, make sure all the pods are deployed and either in the **`Running`** or **`Completed`** state. If they're in `pending` state, wait a few minutes to let the installation and deployment finish.

    Congratulations! You successfully installed Istio into your cluster.

#### [Continue to Exercise 3 - Deploy Guestbook with Istio Proxy](../exercise-3/README.md)
