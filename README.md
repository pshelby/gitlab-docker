# gitlab-docker
docker-compose resources to locally deploy GitLab and GitLab CI runners

## Requirements
* Docker Engine 18.06.0+

## Usage
### Create
Simply run:
```
docker-compose up -d
```

That command will download the Docker images listed in `docker-compose.yml` and start two containers in the background.  The `gitlab` container is the main GitLab app and interface.  `gitlab-runner` is the GitLab CI runner coordinator which communicates with `gitlab` over the created `gitlab` Docker network.

### Clean Up
```
docker-compose down
```

## Issues
If you encounter any issues, feel free to file a [GitHub Issue](https://github.com/pshelby/gitlab-docker/issues) under this repo.
