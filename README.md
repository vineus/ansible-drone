# Drone Ansible Role

Install [drone](https://github.com/drone/drone), [docker](https://www.docker.io/), required and optional docker images for drone operation.

## Requirements

1. Ubuntu 12.04+

## Role Variables

### drone\_images

`drone_images` is a list of hashes, each hash containing the following:

1. `name`: name of the docker repo/image
1. `tag`: repo/image tag to pull. Default 'latest'

### drone\_users

`drone_users` is a list of hashes, each hash containing the following:

1. `name`: Persons name
1. `email`: Persons email
1. `password`: bcrypt password hash (optional, you will have to use forgot password to set a password)
1. `admin`: True/False (boolean). Default False.
1. `state`: present/absent. Default "present"
1. `update_password`: True/False (boolean). Default False. Setting as True will always change the persons password.

#### bcrypt password hash

1. Install `bcrypt` python module
1. `python -c "import bcrypt; print bcrypt.hashpw('<password>', bcrypt.gensalt());"`

### Other settings

1. `drone_github_key`: Github application key
1. `drone_github_secret`: Github application secret
1. `drone_bitbucket_key`: Bitbucket application key
1. `drone_bitbucket_secret`: Bitbucket application secret
1. `drone_smtp_server`: SMTP server address
1. `drone_smtp_port`: SMTP server port
1. `drone_smtp_address`: EMail address to send from
1. `drone_smtp_username`: SMTP authenticaiton username
1. `drone_smtp_password`: SMTP authentication password
1. `drone_hostname`: Hostname that drone will be accessed on. Default hostname defined in inventory or "ansible\_ssh\_password"
1. `drone_open_invitations`: True/False (boolean). Whether open sign up is enabled. Default False.
1. `drone_github_domain`: Github domain. Default github.com
1. `drone_github_apiurl`: Github API url. Default https://api.github.com

### Note

Not all configuration options found in the database are used by drone at this time, or properly configurable by this role.

## Dependencies

1. [docker\_ubuntu](https://galaxy.ansible.com/list#/roles/292)

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    ---
    - hosts: drone
      roles:
        - role: drone
          drone_images:
            - name: bradrydzewski/python
              tag: 2.7
            - name: bradrydzewski/go
              tag: 1.2
            - name: bradrydzewski/php
              tag: 5.5
              state: absent
          drone_users:
            - name: Jim Beam
              email: jim@jimbeam.com
              password: '$2a$12$elB.oZwqu2Ujp.Gi0.3cBOCOpqQ1K5xfNRzxS9AQrtf13.QfvZMO6'
              admin: True
            - name: Jack Daniel
              email: jack@jackdaniels.com
              password: '$2a$12$qSXdN7nCUGHSGaMI/8YyVeWdflr9fjY0/PL1ntr7mKrsVHsKRbMoO'
            - name: Johnnie Walker
              email: johnnie@johnniewalker.com
              state: absent
          drone_hostname: drone.example.com
          drone_github_key: 3c6e0b8a9c15224a8228
          drone_github_secret: 5ebe2294ecd0e0f08eab7690d2a6ee69ccc4a4d8
          drone_smtp_server: localhost
          drone_smtp_port: 25
          drone_open_invitations: True

## License

Apache 2.0
