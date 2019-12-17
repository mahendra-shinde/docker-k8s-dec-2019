## Demo 8: Deploying NGINX Server

1.  Verify if angular is installed in system, if not install it

    ```bash
    $ ng 
    ## IF you get an error! then install it
    $ npm install -g @angular/cli
    ```

2.  Create a new Angular project and build for NGIXN deployment.

    ```bash
    $ mkdir /demo-4
    $ cd /demo-4
    $ ng new app2
    $ cd app2
    ## Build application for deployment on HTTP server
    $ npm run build --prod
    $ cd dist/app2
    ## List all static files
    $ ls
    ```

3.  Create a dockerfile for deploying application on NGINX

    ```ini
    FROM nginx
    WORKDIR /usr/share/nginx/html/

    COPY app2/dist/app2 .
    ## NO ENTRY POINT REQUIRED
    ## USE ENTRY-POINT DEFINED INSIDE BASE IMAGE
    ```

4.  Build an Image and Test Run

    ```bash
    $ cd \demo-4\
    $ docker build -t app2 .
    $ docker run -d -p 8080:80 --name t1 app2
    ```

5.  Test using web browser and then clean up

    http://localhost:8080/
    
    ```bash
    $ docker stop t1
    $ docker rm t1
    ```