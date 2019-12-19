## Config Maps
1. Create a configmap `myconfig.yaml`

    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
        name: myconfig
    data:
        API_URL: http://back-end:8080/api/
        DB_URL: db-connection-string
    ```

2.  Create configmap object using kubectl 

    ```bash
    $ kubectl apply -f myconfig.yaml
    ```

3.  Create a POD (cm-pod.yaml) to USE configmap

    ```yaml
    apiVersion: v1
    kind: Pod
    metadata:
        name: cm-pod
    labels:
        name: cm-pod
    spec:
        containers:
        -   name: cm-pod
            image: nginx:1.7.9
        ### Setting ENVIRONMENT variables
            env:
            -   name: MYNAME
                value: MAHENDRA
        ### IMPORTING ENVIRONMENT variable from configmap
            envFrom:
            -   configMapRef:
                  name: myconfig
        resources:
            limits:
                memory: "100Mi"
                cpu: "100m"
        ports:
        - containerPort: 80
    ```

3.  Deploy the pod and TEST enviornment variables from inside the pod.

    ```
    $ kubectl apply -f cm-pod.yaml
    $ kubectl exec -it cm-pod bash
    $ echo $MYNAME
    $ echo $DB_URL
    $ exit
    ```

4.  Clean up

    ```bash
    $ kubectl delete -f .
    ```