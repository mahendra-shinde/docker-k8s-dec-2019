## Replica Set demo

1.  Create a replicaset using provided YAML [file](./replica-set.yml).

2.  Download the file and run following command to deploy replica set

    ```bash
    $ kubectl apply -f replica-set.yml
    $ kubectl get rs rc1
    $ kubectl get pods -l name=myapp
    ```

3.  Test the `Self Healing` of replica set

    ```bash
    $ kubectl get pods -l name=myapp
    ### Copy the name of FIRST pod from output
    $ kubectl delete pod {PASTE-PODNAME}
    $ kubectl get pods -l name=myapp
    ## The old pod is now replaced with a new one
    ## HINT: Look at AGE property
    ```

4.  Test the Scaling 

    ```bash

    $ kubectl get rs rc1
    ### Output: Desired: 3, Current: 3, Ready: 3
    $ kubectl scale rs rc1 --replicas=10
    $ kubectl get rs rc1
    ## Output: Desired: 10, Current: 10, Ready: 10
    ```