# gitlab-docker
docker-compose resources to locally deploy GitLab and GitLab CI runners

## Requirements
* Docker Engine 18.06.0+

## Usage
### Create
1. Simply run:
```
docker-compose up -d
```

That command will download the Docker images listed in `docker-compose.yml` and start two containers in the background.  Both containers are backed by bind mounts on the host.  The `gitlab` container is the main GitLab app and interface.  `gitlab-runner` is the GitLab CI runner coordinator which communicates with `gitlab` over the created `gitlab` Docker network.

2. After the GitLab container is up and running, proceed to setup the GitLab application and retrieve the GitLab CI runners registration token.
3. Replace `REGISTRATION_TOKEN` in the following runner registration command with the value obtained above and execute:
```
docker run --rm --net gitlab -v `pwd`/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner register \
  --non-interactive \
  --executor "docker" \
  --docker-image alpine:latest \
  --url "http://gitlab/" \
  --registration-token "REGISTRATION_TOKEN" \
  --description "docker-runner" \
  --tag-list "docker" \
  --run-untagged="true" \
  --locked="false" \
  --access-level="not_protected"
```
4. After the runner is successfully registered, add the following lines to [config.toml](gitlab-runner/config/config.toml):
Under **[[runners]]**:
```
clone_url = "http://gitlab/"
```
Under **[runners.docker]**:
```
network_mode = "gitlab"
```


### Clean Up
```
docker-compose down
```
All config, data, and logs will be saved in the host directories previously mapped to the containers.

## Issues
If you encounter any issues, feel free to file a [GitHub Issue](https://github.com/pshelby/gitlab-docker/issues) under this repo.
