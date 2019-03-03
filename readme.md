# Maintaining An Image And Running It As A Container

## How To Build Docker Image And Version It
1. ```cd``` into the directory with a ```Dockerfile```
2. Run the command in CLI 
    ```bash
    docker build --tag <YOUR_IMAGE_NAME_HERE>:<VERSION_NUM> .
    ```
    * This tells Docker to build an image with the name <YOUR_IMAGE_NAME_HERE> from this current directory.
    * https://docs.docker.com/engine/reference/commandline/build/

## How To Push An Image To Docker Hub
1. Run the command in CLI 
    ```bash
    docker push <DOCKER_HUB_ACCOUNT>/<IMAGE_NAME_TO_SEND_TO_DOCKER_HUB>:<VERSION_NUMBER>
    ```
    * You must first build the image with an appropriate tag before pushing to Docker Hub.
    * *Note:* The tag should probably be a version number... eg ```v0.0.1```
2. Once complese this can be viewed online: https://hub.docker.com/r/loganconnor44/memento-scraper-client:

## How To Run A Docker Image In Detached Mode - preferred method
1. Run the command in CLI 
    ```bash
    docker run -d --publish <HOST_PORT_NUM>:<CONTAINER_PORT_NUM> <YOUR_IMAGE_NAME_HERE>
    ```
    * Unforunately, we can not be more explicit with this short flag, because it appears that ```-d``` does not have a full flag, ```--detached```.

### Why Do I Want To Run In Detached Mode?
You get the long container ID for your image and then are kicked back to your terminal.

## How To Run A Docker Container
1. Run the command in CLI 
    ```bash
    docker run --publish <HOST_PORT_NUM>:<CONTAINER_PORT_NUM> <YOUR_IMAGE_NAME_HERE>
    ```
    * This tells Docker to run the image named <YOUR_IMAGE_NAME_HERE> and to publish all container ports to the host machine.
    * When describing the ports the left side is the host port and the right is the container port you have defined in the ```Dockerfile```.
        * <HOST_PORT>:<DOCKER_PORT>

## How To Run A Public Docker Container That Is Available On Docker Hub?
1. Run the command in CLI 
    ```bash
    docker run --publish <HOST_PORT_NUM>:<CONTAINER_PORT_NUM> <DOCKER_HUB_ACCOUNT>/<YOUR_IMAGE_NAME_HERE>:<VERSION_NUMBER>
    ```
    * You may want to run the image in detached mode. Read above in **How To Run A Docker Image In Detached Mode - preferred method**

## How To Version/Tag An Image To Then Publish To The Registry (docker github essentially)
1. Run the command in CLI 
    ```bash
    docker tag <YOUR_LOCAL_IMAGE_NAME> <DOCKER_HUB_ACCOUNT>/<IMAGE_NAME_TO_SEND_TO_DOCKER_HUB>:<VERSION_NUMBER>
    ```
    * The argument after ```tag``` is the name of your local image and the 4th argument is a combination of your Docker Hub account with a repository name : tag name.
    * https://docs.docker.com/get-started/part2/
2. Run the command in CLI 
    ```bash
    docker push <DOCKER_HUB_ACCOUNT>/<IMAGE_NAME_TO_SEND_TO_DOCKER_HUB>:<VERSION_NUMBER>
    ```
    * This references the 4th argument from step one.
    * *Note:* The tag should probably be a version number... eg ```v0.0.1```
3. Once complese this can be viewed online: https://hub.docker.com/r/loganconnor44/memento-scraper-client:

# Starting & Stopping Containers Via Docker Compose Files

## How To Start Multiple Containers Defined In A Docker Compose File
1. ```cd``` into the directory with the ```docker-compose.yml``` file.
2. Run the command in CLI 
    ```bash
    docker-compose up --build
    ```
    * This will spin up your containers and build them fresh.
    * https://docs.docker.com/compose/reference/up/

## How To Stop Multiple Containers Defined In A Docker Compose File
1. ```cd``` into the directory with the ```docker-compose.yml``` file.
2. Run the command in CLI 
    ```bash
    docker-compose down
    ```
    * This will stop your containers.
    * You can also attempt a CNTRL + C in the given terminal to stop - but this does not always stop the containers gracefully.
    * https://docs.docker.com/compose/reference/down/

## How To Remove Database Data Completely
1. ```cd``` into the directory with the ```docker-compose.yml``` file.
2. Run the command in CLI 
    ```bash
    docker-compose down -volumes
    ```
    * This will remove any volumes you that have been mounted to the host machine.
    * https://docs.docker.com/compose/reference/down/

## How To Execute MySql On A Running Container
1. Run the command in CLI 
    ```bash
    docker exec -i <NAME_OF_DOCKER_DB_CONTAINER> mysql -u<MYSQL_USER> -p<MYSQL_PASSWORD> <DESIRED_DATABASE> < <SQL_FILE>
    ```
    * The ```less than``` sign is intended between the desired database and the sql file above.

## How To Copy A File From A Container To The Host Machine (and vise-versa)
1. Identify the container's id
    ```bash
    docker ps
    ```
    or
    ```bash
    docker container ls
    ```
2. After copying the id from the above command's output past it into the below command.
    ```bash
    docker cp <CONTAINER_ID>:./path/to/file/in/container.txt ./path/to/host/file.txt
    ```
    * The full path is necessary.