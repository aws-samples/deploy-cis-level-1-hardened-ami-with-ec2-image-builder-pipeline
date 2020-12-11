RHEL 7 CIS STIG
================

Based on [CIS RedHat Enterprise Linux 7 Benchmark v2.1.1 - 01-31-2017 ](https://community.cisecurity.org/collab/public/index.php).

This repo originated from work done by [Sam Doran](https://github.com/samdoran/ansible-role-stig)

Requirements
------------

You should carefully read through the tasks to make sure these changes will not break your systems before running this playbook.
If you want to do a dry run without changing anything, set the below sections (rhel7cis_section1-6) to false. 

Role Variables
--------------
There are many role variables defined in defaults/main.yml. This list shows the most important.

**rhel7cis_notauto**: Run CIS checks that we typically do NOT want to automate due to the high probability of breaking the system (Default: false)

**rhel7cis_section1**: CIS - General Settings (Section 1) (Default: true)

**rhel7cis_section2**: CIS - Services settings (Section 2) (Default: true)

**rhel7cis_section3**: CIS - Network settings (Section 3) (Default: true)

**rhel7cis_section4**: CIS - Logging and Auditing settings (Section 4) (Default: true)

**rhel7cis_section5**: CIS - Access, Authentication and Authorization settings (Section 5) (Default: true)

**rhel7cis_section6**: CIS - System Maintenance settings (Section 6) (Default: true)  

##### Disable all selinux functions
`rhel7cis_selinux_disable: false`


Dependencies
------------

Ansible > 2.2

Example Playbook
-------------------------

This sample playbook should be run in a folder that is above the main RHEL7-CIS / RHEL7-CIS-devel folder.

```
- name: Harden AMI
  hosts: localhost
  become: yes

  roles:
    - RHEL7-CIS
```

Tags
----
Many tags are available for precise control of what is and is not changed.

Some examples of using tags:

```
    # Audit and patch the file
    ansible-playbook file.yml --tags="patch"
```

License
-------

MIT
