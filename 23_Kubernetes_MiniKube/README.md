## Launch a Single Node Cluster

Minikube is a tool that makes it easy to run Kubernetes locally. Minikube runs a single-node Kubernetes cluster inside a VM on your laptop for users looking to try out Kubernetes or develop with it day-to-day.

More details can be found at https://github.com/kubernetes/minikube

### Assuming Minikube is locally installed

* Check Minikube version

```
$ minikube version
```

* Launch Single Node Kubernetes cluster

```
$ minikube start --wait=false
```

### Gather Kubernetes Cluster Information

The cluster can be interacted with using the kubectl CLI. This is the main approach used for managing Kubernetes and the applications running on top of the cluster.

Details of the cluster and its health status can be discovered via `kubectl cluster-info`

To view the nodes in the cluster using `kubectl get nodes`

If the node is marked as NotReady then it is still starting the components.

This command shows all nodes that can be used to host our applications. Now we have only one node, and we can see that it’s status is ready (it is ready to accept applications for deployment).

### Deploy Containers

Using kubectl run, it allows containers to be deployed onto the cluster: 

```$ kubectl create deployment first-deployment --image=katacoda/docker-http-server```

The status of the deployment can be discovered via the running Pods - `$ kubectl get pods`

Once the container is running it can be exposed via different networking options, depending on requirements. One possible solution is NodePort, that provides a dynamic port to a container.

```
$ kubectl expose deployment first-deployment --port=80 --type=NodePort
```

The command below finds the allocated port and executes a HTTP request.

```
export PORT=$(kubectl get svc first-deployment -o go-template='{{range.spec.ports}}{{if .nodePort}}{{.nodePort}}{{"\n"}}{{end}}{{end}}')
echo "Accessing host01:$PORT"
curl host01:$PORT
```
The result is the container that processed the request.

### MiniKube Dashboard

Enable the dashboard using Minikube with the command ```$ minikube addons enable dashboard```

## References

[KataCoda Scenario](https://www.katacoda.com/courses/kubernetes/launch-single-node-cluster)
