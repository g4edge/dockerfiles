# dockerfiles

![GitHub tag (latest by date)](https://img.shields.io/github/v/tag/g4edge/dockerfiles?logo=git)
![GitHub issues](https://img.shields.io/github/issues/g4edge/dockerfiles?logo=github)
![GitHub pull requests](https://img.shields.io/github/issues-pr/g4edge/dockerfiles?logo=github)
![License](https://img.shields.io/github/license/g4edge/dockerfiles)

Docker containers for building
[pyg4ometry](https://github.com/g4edge/pyg4ometry) wheels based on the
[Manylinux](https://github.com/pypa/manylinux) images. Pre-built images are
available on [Docker Hub](https://hub.docker.com/r/g4edge).

- `ubuntu` is a base image including all required software to build pyg4ometry.
  Used in the pyg4ometry GitHub actions CI
- `pyg4ometry` is based on the `ubuntu` image but includes pyg4ometry too
- `manylinux2014` is a custom image for building pyg4ometry wheels, used in the
  pyg4ometry CI by the cbuildwheel action
- Automated builds are configured on Docker Hub to build `manylinux2014` images
  at every commit or pull request created in this repository (see
  [Docker Hub](https://hub.docker.com/repository/docker/g4edge/manylinux2014_x86_64) >
  Builds > Configure Automated Builds)
- the `bin/build-and-deploy.sh` script can be used to build locally and push
  images to the Docker Hub
