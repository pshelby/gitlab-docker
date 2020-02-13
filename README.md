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

2. After the GitLab container is up and running, proceed to setup the GitLab application and retrieve the GitLab CI runners token.
3. Replace `RUNNERS_TOKEN` in [config.toml](gitlab-runner/config/config.toml) with the value you retrieved from GitLab.

### Clean Up
```
docker-compose down
```
All config, data, and logs will be saved in the host directories previously mapped to the containers.

## Issues
If you encounter any issues, feel free to file a [GitHub Issue](https://github.com/pshelby/gitlab-docker/issues) under this repo.
