# Ubuntu 18.04 LTS (Bionic) Ansible Test Image

[![CI](https://github.com/f-koehler/docker-ubuntu1804-ansible/actions/workflows/build.yml/badge.svg)](https://github.com/f-koehler/docker-ubuntu1804-ansible/actions/workflows/build.yml)
[![Docker Pulls](https://img.shields.io/docker/pulls/fabiankoehler/ubuntu1804-ansible)](https://hub.docker.com/r/fabiankoehler/ubuntu1804-ansible)
[![Docker Image Size (tag)](https://img.shields.io/docker/image-size/fabiankoehler/ubuntu1804-ansible/latest)](https://hub.docker.com/r/fabiankoehler/ubuntu1804-ansible)

Ubuntu 18.04 LTS (Bionic) Docker container for Ansible playbook and role testing.

## Tags

- `latest`: Latest stable version of Ansible.
- `python2`: Deprecated.
- `testing`: Deprecated.

The latest tag is a lightweight image for basic validation of Ansible playbooks.

## How to Build

This image is built on Docker Hub automatically any time the upstream OS container is rebuilt, and any time a commit is made or merged to the `master` branch. But if you need to build the image on your own locally, do the following:

1. [Install Docker](https://docs.docker.com/install/).
2. `cd` into this directory.
3. Run `docker build -t ubuntu1804-ansible .`

> Note: Switch between `master` and `testing` depending on whether you want the extra testing tools present in the resulting image.

## How to Use

1. [Install Docker](https://docs.docker.com/engine/installation/).
2. Pull this image from Docker Hub: `docker pull geerlingguy/docker-ubuntu1804-ansible:latest` (or use the image you built earlier, e.g. `ubuntu1804-ansible:latest`).
3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:ro geerlingguy/docker-ubuntu1804-ansible:latest` (to test my Ansible roles, I add in a volume mounted from the current working directory with `` --volume=`pwd`:/etc/ansible/roles/role_under_test:ro ``).
4. Use Ansible inside the container:
   a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
   b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`

## Notes

I use Docker to test my Ansible roles and playbooks on multiple OSes using CI tools like Jenkins and Travis. This container allows me to test roles and playbooks using Ansible running locally inside the container.

> **Important Note**: I use this image for testing in an isolated environment—not for production—and the settings and configuration used may not be suitable for a secure and performant production environment. Use on production servers/in the wild at your own risk!

## Author

Created in 2018 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
Modified in 2021 by [Fabian Köhler](https://fkoehler.xyz) to include the following modifications:

- include `kmod` package for `modprobe` and friends
- updated GitHub workflow
