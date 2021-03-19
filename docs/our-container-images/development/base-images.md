# Base images

The k8s@home base images are meant to be used as an image to build
all other app container images on top of.

## Distributions

The following distributions are available as a base image:

- [Ubuntu][ubuntu]
- [Alpine][alpine]

The source code can be found [here].

## Tini

The base images use the [Tini][tini] init in order to create the smallest
image possible while still waiting for a child to exit all the while
reaping zombies and performing signal forwarding.

[ubuntu]: https://github.com/orgs/k8s-at-home/packages/container/package/ubuntu
[alpine]: https://github.com/orgs/k8s-at-home/packages/container/package/alpine
[here]: https://github.com/k8s-at-home/container-images/tree/main/base
[tini]: https://github.com/krallin/tini/
