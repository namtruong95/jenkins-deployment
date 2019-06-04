# required package

- docker

- docker-compose

## Bash run docker

```bash
#! init .env
cp .env.example .env
```

```bash
#! install && run docker
docker-compose up -d --build
```

## get /var/jenkins_home/secrets/initialAdminPassword

    ```
    docker exec <docker_id> cat /var/jenkins_home/secrets/initialAdminPassword
    ```

## get init password from docker jenkins

    ```
    docker exec jenkins-deployment_jenkins_1 cat /var/jenkins_home/secrets/initialAdminPassword
    ```

git ls-remote -h git@github.com:namzee95/capistrano-learning.git HEAD

```
bundle install --path vendor/bundle
bundle exec cap frontend:dev deploy
```
