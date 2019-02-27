Notes
=====

Ad-Hoc Commands
---------------

Install nodejs via apt:

    ansible all -m apt -a "name=nodejs state=present" --become

Copy a file

    ansible all -m copy -a "src=/etc/passwd dest=/tmp/passwd"

Create a user

    ansible all -m user -a "name=fred state=present" --become

Stop Service

    ansible all -m service -a 'name=flask-demo state=stopped' --become

Playbooks
---------

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

    ansible-playbook my_playbook.yml --become

### Why two plays?

    One runs as ubuntu---the other as root

