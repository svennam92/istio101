# Exercise 7 - Secure your services

## Mutual authentication with Transport Layer Security (mTLS)

Istio can secure the communication between microservices without requiring application code changes. Security is provided by authenticating and encrypting communication paths within the cluster. This is becoming a common security and compliance requirement. Delegating communication security to Istio (as opposed to implementing TLS in each microservice), ensures that your application will be deployed with consistent and manageable security policies.

Istio Citadel is an optional part of Istio's control plane components. When enabled, it provides each Envoy sidecar proxy with a strong (cryptographic) identity, in the form of a certificate.
Identity is based on the microservice's service account and is independent of its specific network location, such as cluster or current IP address.
Envoys then use the certificates to identify each other and establish an authenticated and encrypted communication channel between them.

Citadel is responsible for:

* Providing each service with an identity representing its role.

* Providing a common trust root to allow Envoys to validate and authenticate each other.

* Providing a key management system, automating generation, distribution, and rotation of certificates and keys.

When an application microservice connects to another microservice, the communication is redirected through the client side and server side Envoys. The end-to-end communication path is:

* Local TCP connection (i.e., `localhost`, not reaching the "wire") between the application and Envoy (client- and server-side);

* Mutually authenticated and encrypted connection between Envoy proxies.

When Envoy proxies establish a connection, they exchange and validate certificates to confirm that each is indeed connected to a valid and expected peer. The established identities can later be used as basis for policy checks (e.g., access authorization).

## Steps

> Version 2 of the guestbook application uses an external service (tone analyzer) which is not Istio-enabled.
> Thus, we will disable mTLS globally and enable it only for communication between internal cluster services in this lab.

1. Ensure Citadel is running

    Citadel is Istio's in-cluster Certificate Authority (CA) and is required for generating and managing cryptographic identities in the cluster.
    Verify Citadel is running:

    ```shell
    kubectl get deployment -l istio=citadel -n istio-system
    ```

    Expected output:

    ```shell
    NAME            DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
    istio-citadel   1         1         1            1           15h
    ```

2. Define mTLS Authentication Policy

    Define mTLS authentication policy for the analyzer service:

```
cat <<EOF | kubectl create -f -
apiVersion: authentication.istio.io/v1alpha1
kind: Policy
metadata:
    name: mtls-to-analyzer
    namespace: default
spec:
    targets:
    - name: analyzer
    peers:
    - mtls:
EOF
```

You should see:
```shell
policy.authentication.istio.io/mtls-to-analyzer created
```

Confirm the policy has been created:
```shell
kubectl get policies.authentication.istio.io
```
Output:
```shell
NAME              AGE
mtls-to-analyzer  1m
```

1. Enable mTLS from guestbook using a Destination rule

```
cat <<EOF | kubectl create -f -
apiVersion: networking.istio.io/v1alpha3
kind: DestinationRule
metadata:
  name: route-with-mtls-for-analyzer
  namespace: default
spec:
  host: "analyzer.default.svc.cluster.local"
  trafficPolicy:
    tls:
      mode: ISTIO_MUTUAL
EOF
```
Output:
```
destinationrule.networking.istio.io/route-with-mtls-for-analyzer created
```

## Verifying the Authenticated Connection

If mTLS is working correctly, the Guestbook app should continue to operate as expected, without any user visible impact. Istio will automatically add (and manage) the required certificates and private keys. To confirm the mTLS traffic, you can launch your Grafana instance and look at the traffic for the analyzer service.

1. Establish port forwarding from local port 8082 to the Grafana instance:

    ```shell
    kubectl -n istio-system port-forward  --address 0.0.0.0 \
      $(kubectl -n istio-system get pod -l app=grafana -o jsonpath='{.items[0].metadata.name}') \
      8082:3000
    ```

2. Click on the web preview icon and select port 8082.
3. Click on Home -> Istio -> Istio Service Dashboard.
4. Select analyzer in the Service drop down.
5. Scroll down to **Incoming Requests by Destination and Response Code**
6. Add more comments to your V2 guestbook application.

![](https://github.com/rvennam/istio101/blob/master/workshop/README_images/mtlsTraffic.png?raw=true)


## Further Reading

* [Basic TLS/SSL Terminology](https://dzone.com/articles/tlsssl-terminology-and-basics)

* [TLS Handshake Explained](https://www.ibm.com/support/knowledgecenter/en/SSFKSJ_7.1.0/com.ibm.mq.doc/sy10660_.htm)

* [Istio Task](https://istio.io/docs/tasks/security/mutual-tls.html)

* [Istio Concept](https://istio.io/docs/concepts/security/mutual-tls.html)

## [Continue to Exercise 8 - Policy Enforcement](../exercise-8/README.md)
