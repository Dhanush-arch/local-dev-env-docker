## local Dev Env Docker
The listed files are used for setting up a local Ubuntu development environment

#### Initial requirements
- Pull the Ubuntu Docker image from Dockerhub if you don't have a local copy of one, using the command ```docker pull ubuntu ```

#### Steps
 1. Navigate to the directory where you wish to create the volume
 2. Place the *Dockerfile* and *docker-compose.yml* file in that directory
 3. Run ``` docker build -t dev-env-img . ``` to build the docker image with the tag *"dev-env-img"*
 4. Run ``` docker-compose run app ``` to start the docker container, which will open a tty
 5. After exiting the docker container, run ``` docker commit -p <container-ID> dev-env-img ``` to commit to a docker image ( This step replaces the existing image with the new image)
 6. To start the environment again, run **step 4**. 

Any changes that are made to the files in the docker container are reflected in the local directory and vice versa. **Step 3** is needed for the initial creation of the image and **step 5** replaces the existing image with the new image. The changes that are made to the environment like
- Updating the system
- Installing / Removing Packages
- Configuration modifications

are not persistent by default in docker. To make the changes persistent, **step 5** commits the current state of the container as a docker image. The *docker-compose.yml* uses the new image to start the environment in the future.

#### Optional Commands
- Run ```docker images``` to list all the docker images in the system
- Run ```docker ps -a``` to list the status of the containers in the system
- Run ```docker rm <container-ID> ``` to remove a container
- Run ```docker rmi <image-ID or tag> ``` to remove a docker image