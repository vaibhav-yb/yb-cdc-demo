# YugabyteDB CDC Pipeline

This repository contains simple steps to set up a YugabyteDB CDC pipeline to get the data from YSQL to a Kafka topic

## Adding your own connector to the image

If you want to use your own custom connector to the docker image, be ready with the jar file which has all the files required for the connector and follow the given steps:

1. Create a directory
  ```sh
  mkdir ~/custom-image
  ```
2. Copy the jar file to the directory
  ```sh
  cp jarFileXYZ.jar ~/custom-image/
  ```
3. Navigate to the directory and create a Dockerfile
  ```sh
  cd ~/custom-image && touch Dockerfile
  ```
4. Edit the contents of the Dockerfile
  ```Dockerfile
  FROM quay.io/yugabyte/debezium-connector:latest
  
  COPY jarFileXYZ.jar $KAFKA_CONNECT_PLUGINS_DIR/debezium-connector-yugabytedb/
  ```
5. Build your docker image
  ```sh
  docker build . -t my-custom-image
  ```
  **NOTE: Do not forget to edit the docker-compose file with this custom image name in case you want to use this newly created image with the docker compose commands**
