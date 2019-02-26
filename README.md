Ansible Presentation
====================


Credentials
-----------

credentials are kept in
aws_user: pygroup
access_key_id: AKIAIY7QGRGEXSEK7EAA

Setup
-----

Create a password

    sudo passwd ubuntu #rayndrop

    # Passwords are not usable after images is launched. Try this:
    echo 'ubuntu:friend' | sudo chpasswd

    Because an "!" is added to /etc/shadow

Remove the writable flag on motd files

    sudo chmod 640 /etc/update-motd.d/*

Edit /etc/ssh/sshd_config

    PasswordAuthentication: yes
    PrintLastLog: no
    Banner: /etc/banner

Create the file at /etc/banner

Generate a keypair:

    ssh-keygen -t rsa -b 4096 -C "littlerock@pythonista.org"

Put the public key in ~/.ssh/authorized_keys

    cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys

Create a symlink from python3 to python

    sudo ln -s /usr/bin/python3 /usr/bin/python

Set ansible host checking to false by creating ~/.ansible.cfg

    [defaults]
    host_key_checking = False

Install rpl

    sudo apt update && sudo apt install rpl

Install pip and venv

    sudo apt install python3-pip python3-venv

Pull repo and install python modules

    cd ~
    git clone git@github.com:jackdesert/ansible-presentation-app
    cd ansible-presentation-app
    python3 -m venv env
    env/bin/pip install flask requests

Symlinks for nginx config and systemd config

    -
    -

Enable systemd unit

    -




Which Images to Use
-------------------

Original Image: ami-39c28c41
pygroup-1:      ami-0845872dfc3cdcdac (most config)
pygroup-10:     ami-03e152304effc1a43 (most config + ~/.ansible.cfg + python symlink)
pygroup-11      ami-021783961b323fadb (includes correct symlink)
pygroup-12      ami-04ac3128fa16bf37e (includes rpl)
pygroup-13      ami-02a0d8064174dd811 (running flask app)


Launch Instances
----------------

    aws ec2 request-spot-instances \
        --spot-price "0.1" \
        --instance-count 1 \
        --block-duration-minutes 60 \
        --launch-specification file://config/spot-request.json


Enable password in Launched Instances
-------------------------------------

When you launch an instance on EC2, the password for the ubuntu user is
disabled. This is represented by a bang in the /etc/shadow file.

After launching the instances, you can reenable the password
using ansible.

### Update /etc/ansible/hosts

First run this:

    aws ec2 describe-instances --filters aws ec2 describe-instances --filters "Name=key-name,Values=bip-pygroup" | grep PublicIpAddress | sudo tee /etc/ansible/hosts


Then open /etc/ansible/hosts and trim it down to the proper format


### Run ad-hoc command to remove bangs

    ANSIBLE_HOST_KEY_CHECKING=False ansible all --private-key=~/.ssh/bip-pygroup.pem --sudo -m shell -a "rpl  "ubuntu:\!" "ubuntu:" /etc/shadow" --user ubuntu



Distribute Paper Copies of Tutorial and IP Addresses
----------------------------------------------------


CHECK
-----

- launch them for a four hour block
  (launch @ 5:30, shuts off @ 9:30)
- Verify can log in from windows

