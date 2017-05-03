Role Name
=========

Ansible role to install (present) or remove (absent) the latest stable nzbget ( http://nzbget.net ) installation.

I wrote this playbook because it was fun. I use a custom (python) module to get the latest stable version number from the nzbget website, I also use a password lookup to geberate a new password, create a stop/start service file in /etc/systemd/system/nzbget.service and added an absent playbook, which removes the installation.

nzbget offers a lot more options and possibilities which are not included in this playbook, the most important obvious is the configuration of a newserver. Open &lt;remote-server&gt;:&lt;control_port&gt; in your browser and login with nzbget and the generated password (see below how to find it).


Requirements
------------

- Linux with systemd
- internet connection (download latest nzbget)
- python[2|3]-requests package installed on the Ansible control machine


Role Variables
--------------

Default variables
- nzbget_state: present

present means install nzbget, can be overruled on command line, see example
- dest_dir: /opt/nzbget

this is where nzbget is installed
- main_dir: /var/lib/nzbget

this is where the downloads end up;
a symbolic link is created to this directory:
<code>{{ dest_dir }}/download -> {{ main_dir}}</code>
might be a good idea to create a filesystem and mount this on /var/lib/nzbget
- control_port: 6789

this is where the nzbget simple webserver is listening, user is nzbget,
the default password is changed (look for ControlPassword in {{ dest_dir }}/nzbget.conf
or run the playbook with -v, then the password is shown on standard output
- group_name: nzbget
- group_gid: 1001
- user_name: nzbget
- user_uid: 1001


Dependencies
------------


Example Playbook
----------------
site.yml:
<pre>
---
- name: install nzbget
  hosts: mediaservers
  become: yes
  roles:
  - nzbget
</pre>
Add nzbget to all hosts in mediaservers group:
<code>ansible-playbook site.yml</code>

Remove nzbget from all hosts in mediaservers group:
<code>ansible-playbook -e nzbget_state=absent site.yml</code>


License
-------

BSD

Author Information
------------------

krahb
btunix.com

