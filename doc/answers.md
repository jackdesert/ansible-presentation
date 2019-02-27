Notes
=====

Pip module:

https://docs.ansible.com/ansible/latest/modules/pip_module.html?highlight=pip

Playbook that Worked for Me
---------------------------




- hosts: all
  become: yes
  become_user: ubuntu
  tasks:
    - pip:
        name: redis
        virtualenv: /home/ubuntu/ansible-presentation-app/env
    - git:
        repo: http://git@github.com/jackdesert/ansible-presentation-app
        dest: /home/ubuntu/ansible-presentation-app
        version: redis-counter

- hosts: all
  tasks:
    - apt:
        name: redis
        state: present
    - systemd:
        enabled: yes
        state: restarted
        daemon_reload: yes
        name: flask-demo.service




### Invoking

    ansible-playbook my_playbook.yml --sudo

### Why two plays?

    One runs as ubuntu---the other as root

