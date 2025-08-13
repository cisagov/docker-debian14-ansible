# Debian 14 (Forky) Ansible Test Image #

[![Build](https://github.com/cisagov/docker-debian14-ansible/actions/workflows/build.yml/badge.svg)](https://github.com/cisagov/docker-debian14-ansible/actions/workflows/build.yml)
[![Docker pulls](https://img.shields.io/docker/pulls/cisagov/docker-debian14-ansible)](https://hub.docker.com/r/cisagov/docker-debian14-ansible/)

Debian 14 (Forky) Docker container for Ansible playbook and role testing.

## Tags ##

  - `latest`: Latest stable version of Ansible, with Python 3.x.

## How to build ##

This image is built on Docker Hub automatically any time the upstream OS container is rebuilt, and any time a commit is made or merged to the `master` branch. But if you need to build the image on your own locally, do the following:

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. `cd` into this directory.
  3. Run `docker build --tag debian14-ansible .`

## How to use ##

  1. [Install Docker](https://docs.docker.com/engine/installation/).
  2. Pull this image from Docker Hub: `docker pull cisagov/docker-debian14-ansible:latest` (or use the image you built earlier, e.g. `debian14-ansible`).
  3. Run a container from the image: `docker run --detach --privileged --volume=/sys/fs/cgroup:/sys/fs/cgroup:rw --cgroupns=host cisagov/docker-debian14-ansible:latest` (to test my Ansible roles, I add in a volume mounted from the current working directory with ``--volume=`pwd`:/etc/ansible/roles/role_under_test:ro``).
  4. Use Ansible inside the container:
    a. `docker exec --tty [container_id] env TERM=xterm ansible --version`
    b. `docker exec --tty [container_id] env TERM=xterm ansible-playbook /path/to/ansible/playbook.yml --syntax-check`

## Notes ##

I use Docker to test my Ansible roles and playbooks on multiple OSes using CI tools like Jenkins and Travis. This container allows me to test roles and playbooks using Ansible running locally inside the container.

> **Important Note**: I use this image for testing in an isolated environment—not for production—and the settings and configuration used may not be suitable for a secure and performant production environment. Use on production servers/in the wild at your own risk!

## Author ##

Nicholas McDonnell - nicholas.mcdonnell@gwe.cisa.dhs.gov

Heavily based on

[geerlingguy/docker-debian13-ansible](https://github.com/geerlingguy/docker-debian13-ansible)
by [Jeff Geerling](https://www.jeffgeerling.com/) AKA [@geerlingguy](https://github.com/geerlingguy).