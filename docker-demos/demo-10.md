## Push an Image to registry


1.  Sign up on docker registry.

    ```bash
    $ docker login
    Username: {DOCKER-ID}
    Password: {PASWORD}
    ```

2.  TAG your images with registry name & Push (upload them)

    ```bash
    $ docker tag app2:latest   mahendrshinde/app2:latest
    $ docker push mahendrshinde/app2:latest
    ```

3.  Sign in on ACR (Azure Container Registry) 

    ```bash
    $ docker login myreg101.azurecr.io
    Username: myreg101
    Password: z=TswowwALRLM1aSw84pj+iNP3bmwYZL
    ```

4.  Re-TAG your image for ACR

    ```bash
    $ docker tag app2:latest myreg101.azurecr.io/mahendra/app2:latest
    $ docker push myreg101.azurecr.io/mahendra/app2:latest
    ```

