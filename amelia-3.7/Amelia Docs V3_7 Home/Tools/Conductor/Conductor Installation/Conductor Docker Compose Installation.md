{% version "3.x" %}
# Overview
This guide will describe the steps to download and run Conductor as a Docker Compose deployment.
# Requirements
-   Docker version 19.03.4+
-   docker-compose version 1.23.1+
# Installation Steps
1.  On the host machine, log in to the IPsoft Docker registry.
    ``` bash
    docker login artifactory.ipsoft.com
    ```
2.  Download the install files from [Artifactory](https://artifactory.ipsoft.com/artifactory/webapp/#/artifacts/browse/tree/General/conductor-docker-compose).  
    It may be necessary to change some of the values in the install script depending on the desired configuration. See the Configuration Options section below.  
3.  Run the install script where `<version>` is a tagged image version available on [Artifactory](https://artifactory.ipsoft.com/artifactory/webapp/#/artifacts/browse/tree/General/conductor).
    ``` bash
    ./docker-compose-conductor.sh <version>
    ```
4.  Use systemd to start the Conductor service.
    ``` bash
    systemctl start conductor
    ```
    Other systemd commands can be used as normal. To stop Conductor run `systemctl stop conductor`. To view all logs from docker-compose `journalctl -u conductor -f` can be used or run `docker-compose logs 'service'` where 'service' is one of the services defined in the `docker-compose.yml` to see individual service logs.
# Configuration Options
## Enable HTTPS
To enable Conductor to be accessed over HTTPS a valid certificate is required. These are typically issued by a known Certificate Authority (CA) and correspond to the domain name you will use to host Conductor.
Configuration Steps
1.  Acquire the .cert and .key file for the certificate you will use. These must be placed in $HOME_DIR/container/ssl.
2.  Generate a 2048 bit DH param file. It is also a good idea to store this file in $HOME_DIR/container/ssl.
    ``` bash
    openssl dhparam -out container/ssl/dhparam-2048.pem 2048
    ```
3.  Update the install script with your file paths
    ``` text
    CONTAINER_FILES=$HOME_DIR/container
    CERT_FILES=$CONTAINER_FILES/ssl
    SSL_CERT=filename.cert
    SSL_KEY=filename.key
    DH_PARAM=dhparam-2048.pem
    ```
## Configuration Variables
This table describes each of the variables found in the install script and what they do. In most installations, these variables should be left to their default value unless explicitly stated otherwise or if the default value causes a problem.
|                          |                                                                 |                                                                                                                                                                                                                |
|--------------------------|-----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name                     | Default                                                         | Description                                                                                                                                                                                                    |
| Host Configuration       |                                                                 |                                                                                                                                                                                                                |
| HOME_DIR                 | The current directory, relative to the location of the script.  | The top-level directory where all Conductor files are stored.                                                                                                                                                  |
| CONTAINER_FILES          | $HOME_DIR/container                                             | The directory where all files copied into the running containers are stored.                                                                                                                                   |
| CERT_FILES               | $CONTAINER_FILES/ssl                                            | The directory for holding files specifically used to enable HTTPS.                                                                                                                                             |
| SSL_CERT                 | [wild.dev.ipsoft.com](http://wild.dev.ipsoft.com).cert          | The filename of the SSL certificate file.                                                                                                                                                                      |
| SSL_KEY                  | [wild.dev.ipsoft.com](http://wild.dev.ipsoft.com).key           | The filename of the SSL certificate key file.                                                                                                                                                                  |
| DH_PARAM                 | dhparam-2048.pem                                                | The filename of the Diffie-Hellman parameters file.                                                                                                                                                            |
| CONDUCTOR_CONFIG_FILE    | application.properties                                          | The filename of the configuration file for the Conductor Spring services.                                                                                                                                      |
| NGINX_CONFIG_FILE        | nginx.conf                                                      | The filename for the configuration file for NGINX.                                                                                                                                                             |
| DOCKER_COMPOSE_YML       | $HOME_DIR/docker-compose.yml                                    | The filename for the Docker Compose file for Conductor.                                                                                                                                                        |
| DOCKER_COMPOSE_BINARY    | \`which docker-compose\`                                        | By default this will find the docker-compose binary on the host. If the binary is not discoverable with 'which' this variable should be changed to the absolute path of the appropriate docker-compose binary. |
| CONDUCTOR_SYSTEMD        | /usr/lib/systemd/system/conductor.service                       | The path to the systemd unit configuration on the host machine.                                                                                                                                                |
| ENV_FILE                 | $HOME_DIR/.env                                                  | The filename for the environment file used by Docker and systemd.                                                                                                                                              |
| Docker Configuration     |                                                                 |                                                                                                                                                                                                                |
| NGINX_CONFIG_PATH        | /etc/nginx/conf.d/default.conf                                  | The path to the default configuration file inside the NGINX container.                                                                                                                                         |
| CONDUCTOR_CONTAINER_PATH | /etc/conductor                                                  | The path to the Conductor directory in each Conductor service container.                                                                                                                                       |
| CONDUCTOR_CONFIG_PATH    | /etc/conductor/config                                           | The path to the configuration directory in each Conductor service container.                                                                                                                                   |
| REPO_URL                 | [artifactory.ipsoft.com](http://artifactory.ipsoft.com)         | The URL of the Docker registry to pull images from.                                                                                                                                                            |
| CONDUCTOR_VERSION        | $1                                                              | The version of Conductor images to pull. This should be supplied to the script as the first and only positional argument.                                                                                      |
| Web Configuration        |                                                                 |                                                                                                                                                                                                                |
| WEB_PORT                 | 80                                                              | The port in which HTTP traffic is served.                                                                                                                                                                      |
| HTTPS_WEB_PORT           | 443                                                             | The port in which HTTPS traffic is served.                                                                                                                                                                     |
| SERVER_NAME              | [conductor01.dev.ipsoft.com](http://conductor01.dev.ipsoft.com) | The URL of the host machine. If using HTTPs this must match the domain corresponding to the certificate.                                                                                                       |
| API Configuration        |                                                                 |                                                                                                                                                                                                                |
| API_HOST                 | api                                                             | The hostname of the conductor_api container.                                                                                                                                                                   |
| API_PORT                 | 8080                                                            | The port exposed by the conductor_api container.                                                                                                                                                               |
| MySQL Configuration      |                                                                 |                                                                                                                                                                                                                |
| DATABASE_HOST            | mysql                                                           | The hostname of the conductor_mysql container.                                                                                                                                                                 |
| DATABASE_PORT            | 3306                                                            | The port exposed by the conductor_mysql container.                                                                                                                                                             |
| DATABASE_USER            | conductor                                                       | The username used by Conductor services to access the MySQL database.                                                                                                                                          |
| DATABASE_PASS            | conductor                                                       | The password for the application database user.                                                                                                                                                                |
| MYSQL_ROOT_PW            | root                                                            | The password for the root database user.                                                                                                                                                                       |
| RabbitMQ Configuration   |                                                                 |                                                                                                                                                                                                                |
| RABBITMQ_HOST            | rabbitmq                                                        | The hostname of the conductor_rabbitmq container.                                                                                                                                                              |
| RABBITMQ_AMQP_PORT       | 5672                                                            | The port exposed by the conductor_rabbitmq container.                                                                                                                                                          |
| RABBITMQ_MGMT_PORT       | 15672                                                           | The port exposed by the conductor_rabbitmq container for the RabbitMQ management interface.                                                                                                                    |
| RABBITMQ_USER            | conductor                                                       | The username of the RabbitMQ user (used by the application and the management interface).                                                                                                                      |
| RABBITMQ_PASS            | conductor                                                       | The password for the RabbitMQ user.                                                                                                                                                                            |
| Redis Configuration      |                                                                 |                                                                                                                                                                                                                |
| REDIS_HOST               | redis                                                           | The hostname of the conductor_redis container.                                                                                                                                                                 |
| REDIS_PORT               | 6379                                                            | The port exposed by the conductor_redis container.                                                                                                                                                             |
# Upgrading Image Versions
When a new version of Conductor is released, the running containers need to be stopped and restarted to pull down the latest versions of the images.
## Upgrade Steps
1.  Run the install script with the new \<version\> to be upgraded to.
    ``` bash
    ./docker-compose-conductor.sh <version>
    ```
2.  Restart the Conductor service to pull the new Docker images and bring up the application.
    ``` bash
    systemctl stop conductor
    systemctl start conductor
    ```
{% /version %}
