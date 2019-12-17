## Demo 7: Build a container image using Dockerfile

1. We will create a new ASP.NET Core Web Application from directory `c:\demos-2\`

    ```pwsh
    $ mkdir \demos-3
    $ cd \demos-3
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
    $ cd \demos-3\app1
    $ dotnet publish -c Release -o publish
    $ cd publish
    ## Test publish artifacts
    $ dotnet app1.dll --urls=http://localhost:8080
    ## Check application using web browser and then stop the application
    $ CTRL + C
    ```

5.  Create a new file `Dockerfile` (Without Extension) in folder `c:\demos-3`

    ```ini
    ## SET the BASE IMAGE 
    FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
    ## COPY the contents of 'publish' folder inside /app directory
    COPY app1/publish /app
    WORKDIR /app
    ENTRYPOINT [ "dotnet","app1.dll" ]
    ```

6.  Use terminal / command prompt to initiate a build

    ```bash
    $ cd /demos-3
    $ docker build -t app1 .
    ## Test the container
    $ docker run --name t2 -d -p 8080:80 app1
    ## Test URL http://localhost:8080
    $ docker stop t2
    $ docker rm t2
    ```