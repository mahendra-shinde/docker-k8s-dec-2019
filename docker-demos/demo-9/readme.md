## Docker Compose demo

1.  Create a new directory `demo-9` and create a `docker-compose.yaml` file inside.

    ```yaml
    version: "3"
    services:
        app:
            image: nginx
            ports: 
            - "80"
            networks: 
            - net1

    networks: 
        net1:
            driver: bridge
            ipam:
                config:
                - subnet: "190.10.0.0/16"  
    ```

2.  From terminal, use following command to create both network and containers

    ```bash
    $ cd demo-9
    ### Validate the YAML file
    $ docker-compose config
    $ docker-compose up -d
    ### Shutdown and destroy
    $ docker-compose down
    ```