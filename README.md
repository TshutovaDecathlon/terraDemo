### 1. Create the directory structure
   
   On your local machine, create the directory for the project to keep the app’s source code and the configuration files.

You can create your own structure, but as a best practice, keep it consistent and informative.

Enter the following commands in the terminal to add the directories:

    Mkdir quickstart_docker
    Mkdir quickstart_docker/application
    Mkdir quickstart_docker/docker
    Mkdir quickstart_docker/docker/application

As a result, your project structure looks like this:

    Quickstart_docker/ # Project directory
	    |-------application/ # Source code of the app
	    |-------docker/ # Add Docker-related files here
		    |-------application/ # Add Dockerfile for the application here

### 2. Create the application 
Add the source code to *quickstart_docker/application directory* as an **application.py** file:

    import http.server
    import socketserver

    PORT = 8000

    Handler = http.server.SimpleHTTPRequestHandler

    httpd = socketserver.TCPServer(("",PORT), Handler)

    print("serving at port", PORT)
    httpd.serve_forever()

### 3. Create the Dockerfile
Docker builds images automatically by reading the instructions from a Dockerfile. It is a text file that contains all commands needed to build a given image.

----
**NOTE**
Do not add any extensions to the file’s name, when you save the Dockerfile

----


 - In your editor open a text file and create the Dockerfile with the following content:


        # Use base image from the registry 
        FROM python:3.5

        # Set the working directory to /app
        WORKDIR /app

        # Copy the 'application' directory contents to the container at /app
        COPY ./application /app

        # Make port 8000 available to services outside this container 
        EXPOSE 8000

        # Execute 'python /app/application.py' when container launches
        CMD ["python", "/app/application.py"]

- Add the Dockerfile to the *quickstart_docker/docker/application* directory. 

For more information on writing dockerfiles, see [Dockerfile](https://docs.docker.com/engine/reference/builder/) reference docs.

### 4. Build the Docker image
In the terminal, run the command: 
    
    docker build -f docker/application/Dockerfile -t exampleapp .   


-f - this option (--file) lets you specify the path to an alternative file, that is not located at the root of the build. The path must be to a file within the build context. If a relative path is specified then it is interpreted as relative to the root of the context.

-t name:tag - this option (--tag) let's you name the resulting image and optionally tag it.

. - this command instructs Docker to build the image using the "context" of the build from the local directory.

For more information on Building Docker images and commands, refer to [Docker](https://docs.docker.com/engine/reference/commandline/build/) reference docs.

To check the result image built, run the command in the terminal: 
	docker images

The result displays the top level images, their repository and tags, and their size:

	REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
	exampleapp   latest    e5b14d14b211   2 hours ago   871MB



## Next Steps 

Read the next section to learn how to upload your Docker image to a repository.