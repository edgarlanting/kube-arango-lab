To try out the kube-arango 1.1.6 k8s operator, setup or use a k8s cluster and follow
the next steps to play around with this awesome product:

`kubectl apply -f 001_arango-crd.yaml`
`kubectl apply -f 002_arango-deployment.yaml`
`kubectl apply -f 003_arango-storage.yaml`
`kubectl apply -f 004_arango-sc.yaml`
`kubectl apply -f 005_arango-single-server.yaml`

Once the above manifests have been applied, check to see if the arangodeployment
and pods are up and running:

`kubectl get pods -o wide -A`
`kubectl get arangodeployments`

Then, to be able to access the ArangoDB server (via the UI), check the service
by running:

`kubectl get service single-server-ea`

This will output something resembling the following:

```
NAME               TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)          AGE
single-server-ea   NodePort   10.96.253.109   <none>        8529:32009/TCP   19m
```

When the service is of the `LoadBalancer` type, use the IP address listed in the `EXTERNAL-IP` column with port `8529`. When the service is of the `NodePort` type, use the IP address of any of the nodes of the cluster, combine with the high (>30000) port listed in the PORT(S) column.

Now you can connect your browser to `https://<ip>:<port>/`.

Your browser will show a warning about an unknown certificate. Accept the certificate for now.

Then login using username root and an empty password.

If you want to delete this setup you can simply roll it back by running:

`kubectl delete -f 001_arango-crd.yaml`
`kubectl delete -f 002_arango-deployment.yaml`
`kubectl delete -f 003_arango-storage.yaml`
`kubectl delete -f 004_arango-sc.yaml`
`kubectl delete -f 005_arango-single-server.yaml`

