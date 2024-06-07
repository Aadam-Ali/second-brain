---
id: 20240614144705
tags: [docker]
---

# Installing `buildx` on MacOS

1. `brew install docker-buildx`
2. `ln -nsf $(which docker-buildx) ~/.docker/cli-plugins/docker-buildx`
3. `docker buildx install` - sets `buildx` as the default builder

Related:
