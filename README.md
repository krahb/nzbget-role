Role Name
=========

Ansible role to install (present) or remove (absent) a nzbget ( http://nzbget.net ) installation

Requirements
------------

OS: Linux with systemd (service file) and internet connection (download latest nzbget)


Role Variables
--------------

Default variables
nzbget_state: present
dest_dir: /opt/nzbget
main_dir: /var/lib/nzbget
control_port: 6789
group_name: nzbget
group_gid: 1001
user_name: nzbget
user_uid: 1001


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

