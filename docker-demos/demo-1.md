### First Docker Demo

1.  Pull an Image from Docker-HUB (Container registry)

    ```bash
    $ docker pull nginx
    ```

2.  Verify the nginx image in local system.

    ```bash
    $ docker images nginx
    ```

3.  Create a new Container using nginx image

    ```bash
    $ docker run -it --name c1 nginx bash
    ```

4.  Check the number of RUNNING containers from a new command prompt.

    ```
    $ docker ps
    ```

5.  Now, let's find IP address of our container and view the nginx welcome page.

    ```
    $ docker inspect c1
    ```

6.  Stop and remove container (Removing container NEVER delete any IMAGE!)

    ```
    $ docker stop c1
    $ docker rm c1
    ```

