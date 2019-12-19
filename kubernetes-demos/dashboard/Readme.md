### For Installing Kubernetes Dashboard

1.  Run the YAML file to deploy kubernetes dashboard application.

    ```bash
    $ kubectl apply -f kubernetes-dashboard.yaml
    $ kubectl get deploy -n kube-system
    ```

2.  Create a new Service Account (User account for Applications) with RoleBinding

    ```bash
    ### Allow Kubernetes Dashboard to collect facts from cluster
    $ kubectl apply -f role-binding.yml
    ### Allow NEW User to connect kubernetes dashboard
    $ kubectl apply -f admin-user.yaml
    ```

3.  Start the PROXY Server to access kubernetes API Server.

    ```bash
    $ kubectl proxy 
    ```

4.  Use web-browser to connect this URL: 
    http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/#

    > This URL is ACCESSIBLE ONLY TILL `kubectl proxy` COMMAND IS RUNNING


5.  Open new terminal and try to get TOKEN

    ```bash
    $ kubectl describe serviceaccount mahendra -n kube-system
    ## Note down the TOKE NAME which should be similar to  mahendra-token-5jssk
    $ kubectl describe secret -n kube-system  mahendra-token-5jssk
    ## copy the token string
    ```

6.  Go back to web browser, use TOKEN for login, paste the token in field.