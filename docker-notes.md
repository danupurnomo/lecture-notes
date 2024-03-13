# DOCKER NOTES

---
# A. Installation
- Main source : https://docs.docker.com/desktop/
- Please install based on the specifications of the computer you are using.
- If the computer version you are using does not meet the minimum requirements from the official source, you can still install docker with Docker Toolbox. 
- For more information about Docker Toolbox, please read [source 1](https://www.upwork.com/resources/docker-toolbox) and [source 2](https://nickjanetakis.com/blog/should-you-use-the-docker-toolbox-or-docker-for-mac-windows).
- To verify installation, open Commnd Prompt or Terminal, and type `docker`. If the installation is successful, a list of Docker commands will appear.

---
# B. Tutorial
You can use some of the sources below to learn more about Docker :
1. [Docker 101 Tutorial](https://www.docker.com/101-tutorial/)
   
2. [Docker-curriculum.com](https://docker-curriculum.com/)

---
# C. Syntax
## C.1 - Basic Syntax
1. Get list of Docker command
   ```
   $ docker
   ```

2. Check Docker version
   ```
   $ docker --version
   ```

3. Run a Docker Image from DockerHub
   ```
   $ docker run hello-world
   
   try this too
   $ docker run hello-seattle
   ```

## C.2 - Docker Image
4. Build a Docker Image from Dockerfile
   ```
   Syntax  : $ docker build -t <app-name>:<tag> .
   
   Example : $ docker build -t my-game:v0.0.1 .
   ```

5. Change tag of a Docker Image
   ```
   Syntax  : $ docker tag <app-name>:<old-tag> <app-name>:<new-tag>

   Example : $ docker tag my-game:v0.0.1 my-game:v0.0.2
   ```

6. Run a Docker Image
   ```
   Syntax  : $ docker run [options] <app-name>:<tag>
   Example : $ docker run -it my-game:v0.0.1
   ```
   For more details about `docker run` or `[options]`, please visit [the official documentation](https://docs.docker.com/engine/reference/run/).

7. List all Docker Images
   ```
   Syntax : $ docker images
   ```

## C.3 - Docker Container


8. List all Docker Container
   ```
   Syntax : $ docker ps -a
   ```

9. Run existing container
   ```
   Syntax    : $ docker start [options] <container-name or container-id>
   Example 1 : $ docker start -ai quizzical_hawking
   Example 2 : $ docker start -ai fd1a7b37a93e
   ```

10. Check CPU & memory usage
    ```
    Syntax : $ docker stats
    ```

11. Check disk space usage
    ```
    Syntax : $ docker system df
    ```

12. Delete a Docker Container
    ```
    Syntax    : $ docker rm <container-name or container-id>
    Example 1 : $ docker rm quizzical_hawking
    Example 2 : $ docker rm fd1a7b37a93e
    ```

13. Delete all Docker Containers
    ```
    Syntax : $ docker rm $(docker ps -aq)
    ```

14. Delete a Docker Image
    ```
    Syntax  : $ docker rmi <image-id> or $ docker rmi <image-name>:<tag>
    Example 1 : $ docker rmi afa783ad460f
    Example 2 : $ docker rmi my-game:v0.0.1
    ```

15. Delete all Docker Images
    ```
    Syntax : $ docker rmi -f $(docker images -q)
    ```
---
# D. Push to DockerHub
1. Login to DockerHub
   ```
   Syntax : $ docker login
   ```

2. Create tag between image that you want to push and repository in DockerHub
   ```
   Syntax  : $ docker tag <image-id> <dockerhub-username/image-name/tag>
   Example : $ docker tag afa783ad460f danusogipurnomo/my-game:v0.0.1
   ```
   
3. Push to Docker Hub
   ```
   Syntax  : $ docker push <dockerhub-username/image-name/tag>
   Example : $ docker push danusogipurnomo/my-game:v0.0.1
   ```

4. If you experience an error like the following :
   ```
   denied: requested access to the resource is denied
   ```
   
   log out first with the syntax below then repeat step 1 to step 3
   ```
   Syntax : $ docker logout
   ```

5. To test the image that has been pushed
   *Make sure that on your computer there are no more images that are the same as the image you just pushed*
   ```
   Syntax  : $ docker run [options] <dockerhub-username/image-name/tag>
   Example : $ docker run -it danusogipurnomo/my-game:v0.0.1
   ```