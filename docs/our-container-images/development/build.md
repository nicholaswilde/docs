# Build

Building of the container images need to be done from the root directory of the
repository so that the app files, such as [entrypoint.sh], can be properly
[copied](./dockerfile.md#copy) into the image.

## Task

[Task][task] may be used to semi-automate the building and loading of a
container image.

The `APP` parameter will need to be set in order to tell Task which app needs
to be processed.

Run the following command from the root directory of the repository.

```shell
task build APP=<app name>
```

Other tasks can be listed by running `task -l`.

## Manual

The container images can be built and loaded manually by using the Docker cli
from the repository root directory.

### Build

```shell
docker buildx build --build-arg VERSION=$(cat ./apps/<app name>/VERSION) --platform $(cat ./apps/<app name>/PLATFORM) -f ./apps/<app name>/Dockerfile .
```

### Load

```shell
docker buildx build -t <app name>:test --build-arg VERSION=$(cat ./apps/<app name>/VERSION) -f ./apps/<app name>/Dockerfile . --load
```

[entrypoint.sh]: ./creating-a-new-container-image.md#entrypointsh
[task]: https://github.com/go-task/task
