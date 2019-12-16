## Volume demo

1. Create named volume, get location of volume.

    ```bash
    $ docker volume create vol1
    $ docker inspect vol1
    ```

2.  Create a temporary container to copy files inside the volume.

    ```bash
    $ docker run --name t1 -it -v vol1:/data   nginx   bash
    ```

3.  Open new terminal / command prompt to copy the files

    ```bash
    $ docker cp .\myapp1\*   t1:/data/
    $ docker stop t1
    $ docker rm t1
    ```
4.  Launch a new nginx container

    ```bash
    $ docker stop c1 c2
    $ docker rm c1 c2
    $ docker run --name c1 -d -v vol1:/usr/share/nginx/html/ -p 8080:80  nginx  
    $ docker run --name c2 -d -v vol1:/usr/share/nginx/html/ -p 8081:80  nginx  
    ```

5.  Access both containers using following URLs from web browser:

    http://localhost:8080
    http://localhost:8081


6.  Modify the files inside myapp1 and then repeat steps #2 and #3.