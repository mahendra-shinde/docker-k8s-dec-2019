## Demo 6 : Building Container image from Docker CLI

Building an image using docker-CLI
1. Use base image to create a temporary container.
2. Copy the application files inside running container.
3. Test the application.
4. Using `docker commit` command capture the R/W layer of container 
    into a new read-only layer and create new image.
5. Use new image to create container
6. Delete the containers


1. We will create a new ASP.NET Core Web Application from directory `c:\demos-2\`

    ```pwsh
    $ mkdir \demos-2
    $ cd \demos-2
    $ dotnet new mvc -n app1
    $ cd app1
    ## Test run the application
    $ dotnet run
    ## Stop the application
    $ CTRL + C
    ```

2.  Open the `app1\app1.csproj` and note down the ASP.NET Runtime version used by this project.
    My project is using asp.net core 3.1

3.  Pull a container image matching the asp.net core runtime version with project.

    ```pwsh
    #### FOR ASP.NET CORE 3.1
    $ docker pull mcr.microsoft.com/dotnet/core/aspnet:3.1
    #### FOR ASP.NET CORE 2.2
    $ docker pull mcr.microsoft.com/dotnet/core/aspnet:2.2
    ```

4.  Create the PUBLISH artifacts for your project.

    ```pwsh
    $ cd \demos-2\app1
    $ dotnet publish -c Release -o publish
    $ cd publish
    ## Test publish artifacts
    $ dotnet app1.dll --urls=http://localhost:8080
    ## Check application using web browser and then stop the application
    $ CTRL + C
    ```

5.  Create a new temporary container.

    ```bash
    $ docker run --name t1 -it -p 8080:80 mcr.microsoft.com/dotnet/core/aspnet:3.1 bash
    ```

6.  Create another terminal or command prompt

    ```bash
    $ cd \demos-2\app1
    ## Copy all files / folders from PUBLISH directory to container
    $ docker cp -a C:\demos-2\app1\publish\ t1:/app
    ```

7.  Switch back to first terminal (Step #5)

    ```bash
    $ cd /app
    ## Verify all files from PUBLISH directory
    $ dir
    $ dotnet app1.dll --urls=http://0.0.0.0:80
    ```

8.  Test application from web-browser

    http://localhost:8080

9.  Now if Application works correctly, use terminal from step# 5/7 to end the container.

    ```bash
    $ exit
    $ docker commit t1 aspnet-sample:3.1
    ```

10. Now, you have a new container image which can be used for creating container instances.

    ```bash
    $ docker rm t1
    ## Test the new image
    $ docker run -d -p 8080:80 aspnet-sampleapp:3.1 dotnet /app/app1.dll --urls=http://0.0.0.0:80
    ```

11. Now, Again access your application from web browser `http://localhost:8080`

12. Clean Up

    ```bash
    $ docker stop $(docker ps -q)
    $ docker rm $(docker ps -aq)
    ```