hxpro.selinux
=============

set selinux fact (boolean) true if selinux is Enforced
Install packages for SELinux enforced system


Example Playbook
----------------

    - hosts: servers
      roles:
          - { role: hxpro.selinux }
      tasks:
          - include: my_selinux_tasks.yml
            when: selinux

License
-------

[WTFPL](https://raw.githubusercontent.com/hxpro/ansible-role-selinux/master/LICENSE)

Author Information
------------------

Matěj Koudelka <matej@hxpro.cz>
