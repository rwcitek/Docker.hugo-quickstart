# Docker.hugo-quickstart
Docker image of a Hugo server with the Quickstart example included.

The image is hosted on [Docker Hub](https://hub.docker.com/repository/docker/rwcitek/hugo-quickstart).


## Run a container instance
```bash
docker run -d --name hugo -p 1313:1313 rwcitek/hugo-quickstart
```

Open a browser and navigate to ...
- http://localhost:1313           # on anything, but a Chromebook
- http://penguin.linux.test:1313/ # on a Chromebook


## Exec into the container to look around
```bash
docker exec -it hugo /bin/bash
```


## Show the Hugo folder structure, three levels deep
```bash
docker exec hugo tree -L 3 /work/
```


## To add your own posts
```bash
docker run -d \
  --name hugo \
  -v ${PWD}/my_posts/my_own_post.md:/work/quickstart/content/posts/my_own_post.md \
  -p 1313:1313 \
  rwcitek/hugo-quickstart
```


## To replace the default posts folder with your own
The same can be done with any other Hugo folder, e.g. themes.
```bash
docker run -d \
  --name hugo \
  -v ${PWD}/my_posts/:/work/quickstart/content/posts/ \
  -p 1313:1313 \
  rwcitek/hugo-quickstart
```


## Stop and remove the container
```bash
docker container stop hugo
docker container rm hugo
```


## Build the image
```bash
docker build --tag rwcitek/hugo-quickstart docker/
```

