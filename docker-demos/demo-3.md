## Demo 3 Networking

1.  Stop and delete all containers (DOES NOT WORK WITH CMD, User Powershell)

    ```bash
    ### Find all CONTAINERS (-q for Displaying only ID, -a for ALL Containers)
    $ docker stop $(docker ps -q)
    $ docker rm $(docker ps -aq)
    ```

2.  List all networks 

    ```bash
    $ docker network ls
    ```

3.  Try create a container in NONE network

    ```bash
    $ docker run -d --name c1 --net none nginx
    $ docker inspect c1 
    ##### Observe: No IP Address assigned to container!!!
    $ docker stop c1
    $ docker rm c1
    ```

4.  try create a container in HOST network

    ```bash
    $ docker run -d --name c1 --net host nginx
    $ docker inspect c1 
    ##### Observe: No IP Address assigned to container!!!
    $ docker stop c1
    $ docker rm c1
    ```

5.  Clean Up (Use step #1)

6.  Creating a new Bridge Network

    ```bash
    $ docker network create mynet1 -d bridge --subnet 180.18.0.0/16
    $ docker network ls
    $ docker inspect mynet1
    ```

7. Create TWO containers in network `mynet1` and try to ping each other

    ```bash
    $ docker run --name c1 --net mynet1 -d nginx 
    $ docker run --name c2 --net mynet1 -it mahendrshinde/mysql-client bash
    $ curl http://c1
    ```

8.  Open another terminal / command prompt and try following:

    ```bash
    $ docker inspect mynet1
    ## Note down the IP address of container c1
    ```

9.  Switch back to terminal / command prompt running container `c2`

    ```bash
    $ curl http://{C1 IP Address}
    ```

10. Clean Up

    ```bash
    $ docker stop c1 c2
    $ docker rm c1 c2
    ```
    
