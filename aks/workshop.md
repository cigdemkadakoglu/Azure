# AZURE KUBERNETES SERVICE - WEBASSEMBLY WORKSHOP - 1

## Creating WebAssembly System Interface (WASI) node pools in Azure Kubernetes Service (AKS) to run your WebAssembly (WASM) workload

1 . Install aks-preview extensions.

```bash
az extension add --name aks-preview
```

2. Update the latest version of the extension.

```bash
az extension update --name aks-preview
```

3. Register the feature for WasmNodePoolReview.

```bash
az feature register --namespace Microsoft.ContainerService --name WasmNodePoolPreview
```

4. Verify the feature for WasmNodePoolReview.

```bash
az feature show --namespace Microsoft.ContainerService --name WasmNodePoolPreview
```

5. Provider the feature.

```bash
az provider register --namespace Microsoft.ContainerService
```

6. Add a nodepool.

```bash
az aks nodepool add --resource-group $RESOURCE_GROUP --cluster-name $AKS_NAME --name $POOL_NAME --node-count 1 --workload-runtime WasmWasi
```

7. Show the nodepol.

```bash
az aks nodepool show -g $RESOURCE_GROUP --cluster-name $AKS_NAME -n $POOL_NAME --query workloadRuntime
```

8. Check the cluster nodes.

```bash
kubectl get nodes -o wide
```

9. Describe the wasi node.

```bash
kubectl describe node $NODE_NAME
```

10. Apply the yaml.

```bash
kubectl create -f test.yaml
```

11. Check the application.

```bash
curl http://EXTERNAL_IP:port/hello
```

12. Check the services in the cluster.

```bash
kubectl get svc
```

13. Delete the application.

```bash
kubectl delete -f test.yaml
```

14. Delete the node pool from the AKS cluster.

```bash
az aks nodepool delete --name $POOL_NAME -g $RESOURCE_GROUP --cluster-name $AKS_NAME
```
















