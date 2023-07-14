# NodePort Service in Kubernetes

This README.md file provides an overview of NodePort service in Kubernetes, explaining its purpose, usage, creation process, and provides an example YAML configuration.

## What does a NodePort service do?

In Kubernetes, a NodePort service is a way to expose a specific application running on a cluster to the outside world. It maps a specific port on each cluster node to a target port within the service. This allows external traffic to reach the application running inside the cluster.

## Why do we use NodePort in Kubernetes?

NodePort is used in Kubernetes to enable access to services running within the cluster from outside the cluster. It provides a static port that is open on every node in the cluster, which can be used to access the service. This is useful in scenarios where external clients or services need to communicate with applications running inside the cluster.

## How to create a NodePort service?

To create a NodePort service in Kubernetes, you need to define a Service resource in a YAML file. Here are the steps to create a NodePort service:

1. Create a YAML file (e.g., `nodeport-service.yaml`) and open it in a text editor.
2. Define the API version, kind, metadata, and spec for the Service resource.
3. Set the `type` field to `NodePort` in the spec section.
4. Specify the `port` field with the desired target port for the service.
5. Optionally, define the `nodePort` field to specify a specific port number (within the allowed range) for the node.
6. Save the file.

Once you have the YAML file ready, you can apply it to your Kubernetes cluster using the `kubectl` command:

```shell
kubectl apply -f nodeport-service.yaml
```

The NodePort service will be created, and you can use it to access your application from outside the cluster.

## What is the range of NodePort service?

In Kubernetes, the range for NodePort service is from 30000 to 32767. By default, if you don't specify the `nodePort` field in your Service YAML, Kubernetes will automatically assign a port within this range. However, if you need to specify a specific port number, make sure it falls within this range.

## Example YAML for NodePort Service

Here's an example YAML configuration for creating a NodePort service in Kubernetes:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  type: NodePort
  ports:
    - port: 8080
      targetPort: 80
      nodePort: 32000
  selector:
    app: my-app
```

In this example, I define a NodePort service named `my-nodeport-service`. The service listens on port `8080` and forwards the traffic to the target port `80` within the service. The `nodePort` field is set to `32000`, specifying a specific port within the allowed range. Finally, the selector field is used to target pods with the label `app: my-app`.

Remember to modify the YAML file according to your application's specific requirements before applying it to your Kubernetes cluster.

## Conclusion

NodePort service in Kubernetes provides a way to expose applications running within a cluster to external clients or services. By following the steps mentioned above, you can easily create a NodePort service and start accessing your application from outside the cluster.
