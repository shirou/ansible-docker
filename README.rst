Ansible docker testing on CircleCI
=============================================

What's this
--------------

This is an sample repository to test ansible inside the docker container on the CircleCI. This example user **docker connection plugin**, so you does not need to install sshd container inside.

`inventory_docker` is an inventory directory to load both static and dynamic inventory.


Explaining circle.yml 
--------------------------------

::

    - docker run -d --name web ubuntu:16.04 /bin/sleep 3600

This line means start ubuntu:16.04 image with `web` name. Ansible docker dynamic inventory returns group with this name.

Here is a part of JSON which dynamic inventory returnes.

::

  "web": [
    "web"
  ],
  "image_ubuntu:16.04": [
    "web"
  ],
  "33220114d5bed36e03dfac72d52ae115a2da12f3e08b995325182398aae2a95a": [
    "web"
  ],
  "33220114d5bed": [
    "web"
  ],
  "running": [
    "web"
  ],
  "docker_hosts": [
    "unix://var/run/docker.sock"
  ],
  "unix://var/run/docker.sock": [
    "web"
  ],

The point is, set container name to your actual group. `web` in this case. It makes your playbook stable.

::

    - ansible-playbook -i inventory_docker web.yml.

And run ansible-playbook command.



