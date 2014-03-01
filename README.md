Drone
=====

Install [drone](https://github.com/drone/drone), [docker](https://www.docker.io/), required and optional docker images for drone operation.

Requirements
------------

1. Ubuntu 12.04+

Role Variables
--------------

1. `drone_images` is a list of hashes, each hash containing the `name` of the docker repo/image and an optional `tag`, containing the version. If no `tag` is specified `latest` is assumed.

Dependencies
------------

1. [docker_ubuntu](https://galaxy.ansible.com/list#/roles/292)

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    ---
    - hosts: drone
      roles:
        - role: drone
          drone_images:
            - name: bradrydzewski/python
              tag: 2.7

License
-------

Apache 2.0
