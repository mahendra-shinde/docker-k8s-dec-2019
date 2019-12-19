## Setup Helm

1. Download Helm for Windows (v 2.15)

    https://get.helm.sh/helm-v2.15.2-windows-amd64.zip

2.  Extract the contents of ZIP into C:\helm directory

3.  Open command prompt inside c:\helm and initialize helm environment.

    ```bash
    $ helm init
    ```

4.  Search for Helm Chart for MYSQL Database

    ```bash
    $ helm search mysql
    $ mkdir sample
    ## Download the helm chart 'stable/mysql' and extract it
    ## inside sample directory
    $ helm fetch stable/mysql -d sample --untar
    $ cd sample/mysql
    ## To deploy your helm-chart goback to sample
    $ cd \helm\sample
    ### helm install --name {RELEASE-NAME} {CHART-DIRECTORY/TAR-Ball}
    $ helm install --name mydb mysql
    ## Clean Up
    $ helm delete mydb
    ```

5.  Fresh helm chart from scrach

    ```bash
    $ cd sample
    $ helm create myapp1
    $ code myapp1
    ```

6.  Modify 'values.yaml' file 

    ```yaml
    replicaCount: 3

    image:
    repository: mahendrshinde/hostname
    tag: node
    pullPolicy: IfNotPresent
    service:
    type: LoadBalancer
    port: 8080

    container:
    port: 3000
    ```

7.  Open `templates/deployment.yaml` to add new variable `.container.port`

    ```yaml
    containers:
    - name: {{ .Chart.Name }}
        image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
        imagePullPolicy: {{ .Values.image.pullPolicy }}
        ports:
        - name: http
            containerPort: {{ .Values.container.port }}
            protocol: TCP
    ```
    > This is a partial view of original deployment.yaml
        please change second last line from `containerPort: 80` to `containerPort: {{ .Values.container.port }}`
    
8.  Install this chart from helm CLI

    ```bash
    $ helm install --name app1 myapp1
    ```

9.  Access application using web browser `http://localhost:8080`

10. Clean Up

    ```bash
    $ helm delete app1
    ```