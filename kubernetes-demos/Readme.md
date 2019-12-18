## Creating custom namespace

1.  Create a file with name `namespace-1.yml` and following lines:

    ```yaml
    apiVersion: v1
    kind: Namespace
    metadata:
        name: mahendra
    ```

2.  Use `kubectl` to deploy this yaml to kubernetes cluster.

    ```bash
    $ kubectl apply -f .\namespace-1.yml
    $ kubectl get namespaces
    ```

3.  Clean Up : deleting a namespace

    ```bash
    $ kubectl delete -f .\namespace-1.yml
    ## OR ####
    $ kubectl delete namespace mahendra
    ```