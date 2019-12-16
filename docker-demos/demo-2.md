## Demo 2

1.  Create a new NGINX container in DETACHED mode and Host port 8080

    ```
    $ docker stop c2
    $ docker rm c2
    $ docker run -d -p 8080:80 --name c2 nginx
    ```

2.  Test the application using web browser:

    http://localhost:8080


3.  View the application log (if any) from command line

    ```bash
    $ docker logs c2
    ```

4.  Now, create one HTML file in current directory with name `index.html`
5.  Use following command to copy `index.html` from current directory to inside container filesystem.

    ```bash
    $ docker cp .\index.html c2:/usr/share/nginx/html/
    ```

    > The container fs path /usr/share/nginx/html/ is location of DEFAULT webapp in nginx, If you use IIS server, then path is /inetpub/wwwroot/

6.  refresh the webpage http://localhost:8080/