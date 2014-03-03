# Drone Ansible Role

Install [drone](https://github.com/drone/drone), [docker](https://www.docker.io/), required and optional docker images for drone operation.

## Requirements

1. Ubuntu 12.04+

## Role Variables

### Upgrades

Drone does not currently offer an apt repository, to upgrade to a new verison supply `--extra-vars upgrade_drone=true` with your `ansible-playbook` run.

### drone\_images

`drone_images` is a list of hashes, each hash containing the following:

* `name` name of the docker repo/image
* `tag` repo/image tag to pull. Default `latest`

### drone\_users

`drone_users` is a list of hashes, each hash containing the following:

* `name` Persons name
* `email` Persons email
* `password` bcrypt password hash (optional, you will have to use forgot password to set a password)
* `admin` True/False (boolean). Default `False`.
* `state` present/absent. Default `present`
* `update_password` True/False (boolean). Default `False`. Setting as True will ensure the specified password.

#### bcrypt password hash

1. Install `bcrypt` python module
1. `python -c "import bcrypt; print bcrypt.hashpw('<password>', bcrypt.gensalt());"`

### Email

* `drone_smtp_server` SMTP server address
* `drone_smtp_port` SMTP server port
* `drone_smtp_address` EMail address to send from
* `drone_smtp_username` SMTP authenticaiton username
* `drone_smtp_password` SMTP authentication password

### GitHub

* `drone_github_key` GitHub application key
* `drone_github_secret` GitHub application secret.
* `drone_github_domain` GitHub domain. Default `github.com`
* `drone_github_apiurl` GitHub API url. Default `https://api.github.com`

### Daemon

* `drone_hostname` Hostname that drone will be accessed on. Default hostname defined in inventory or "ansible\_ssh\_password"
* `drone_port` Port for drone to listen on
* `drone_scheme` http or https (https requires `drone_sslcert` and `drone_sslkey` and probably `drone_port` configured for `443`)
* `drone_sslcert` Path to SSL certificate
* `drone_sslkey` Path to SSL key

### Other

* `drone_open_invitations` True/False (boolean). Whether open sign up is enabled. Default `False`.


### Note

Not all configuration options found in the database are used by drone at this time, or properly configurable by this role.

## Dependencies

1. [docker\_ubuntu](https://galaxy.ansible.com/list#/roles/292)

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    ---
    - hosts: drone
      roles:
        - role: sivel.drone
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
          drone_scheme: https
          drone_port: 443
          drone_sslcert: /etc/drone/ssl.crt
          drone_sslkey: /etc/drone/ssl.key
          drone_github_key: 3c6e0b8a9c15224a8228
          drone_github_secret: 5ebe2294ecd0e0f08eab7690d2a6ee69ccc4a4d8
          drone_smtp_server: localhost
          drone_smtp_port: 25
          drone_open_invitations: True

## License

Apache License, Version 2.0
