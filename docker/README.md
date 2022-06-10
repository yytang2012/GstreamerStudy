### Build the docker image 
```shell
docker-compose up --build
```


### Download the Clion-*.tar.gz to docker/data from [Clion](https://www.jetbrains.com/clion/download/#section=linux)


### Enter the container and install Clion
```shell
docker exec -it container-deepstream-clion-1.0 /bin/bash
```

## In Container
1. Extract Clion
    ```shell
    cd /project/docker/data/ && tar -xf CLion-*.tar.gz -C /opt/
    ```
2. Install Clion
    ```shell
    cd /opt/clion-*/bin && ./clion.sh
    ```
