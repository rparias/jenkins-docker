# Jenkins Docker Image with Docker

This is a repo with Docker files to create a Jenkis container with docker inside.

## Installation

### Before to build the Dockerfile

You need a folder that will work like a volume in your host machine:

```bash
mkdir ~/jenkins_home
sudo ln -s ~/jenkins_home /var
```

### After the container is running

To check if docker is running inside the container, you can execute docker ps inside the container, but a permission denied error could happen, to solve this, execute the following commands like a root:

```bash
docker-compose exec -u 0 jenkins bash
usermod -aG docker jenkins
chmod 666 /var/run/docker.sock
sudo service docker restart
docker-compose exec jenkins bash
```

Now you can enter with jenkins user

```bash
docker-compose exec jenkins bash
docker ps
```

After the steps above you can execute docker inside the container.

## Needed plugins for pipelines with docker

Install the following plugins on jenkins:

- Docker
- Docker Pipeline

## Example of declarative pipeline

```groovy
pipeline {
    agent { docker { image 'maven:3.3.3' } }
    stages {
        stage('build') {
            steps {
                sh 'mvn --version'
            }
        }
    }
}
```
