Using Ansible
=============

Docs: docs.ansible.com/ansible


1. Get a (paper) list of IP addresses
-------------------------------------

These machines are for you to use.
Choose one of them to be your master box.

2. Log in to the master box
---------------------------

    ssh ubuntu@ip-address-from-master-box

password: rayndrop
(notice the misspelling)


3. Install Ansible
------------------

    sudo apt install ansible

4. Set up Hosts File
--------------------

    sudo vi /etc/ansible/hosts

alternatively:

    sudo nano /etc/ansible/hosts

Put all the IP addresses EXCEPT your master box in the file.
Format goes like this:

    <IP>
    <IP>
    <IP>
    etc.

5. Ping your hosts
------------------

    ansible all -m ping


6. What was set up already to allow this to happen?
---------------------------------------------------

Run these commands if you want to see what

    cat ~/.ansible.cfg
    cat ~/.ssh/authorized_keys


