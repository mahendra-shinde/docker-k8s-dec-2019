## Demo 5 : Volumes

## Please allow docker to access D: or C: drive from Docker Settings.
## Right Click on Docker Desktop Icon (In System Tray) > Settings
## Goto SharedDrive and Choose D:\ (or C:\ Drive) and click apply
## You would be prompted to enter Windows Admin account and password.

1.  Create a first container with Volume mount

    ```bash
    docker run -d -v d:\git\docker-k8s-dec-2019\docker-demos\myapp1:/usr/share/nginx/html/ -p 8080:80 nginx
    ```

    > Note: replace host path `d:\git\docker-k8s-dec-2019\docker-demos\myapp1` with folder path which contains your `index.html` file

2.  Test Application using URL http://localhost:8080

3.  Make some changes to `index.html` file in local system and refresh your browser (http://localhost:8080).