# ASPP laptop installation helpers

## How to install

There are two main playbooks in this repository:

`setup-ansible.yml`, which creates the ansible-pull timer and services on a
computer but does not activate them.

`all.yml`, which enables and starts the timers and then does a full
installation of the ASPP laptop.

Depending on whether the installation should be done on a disk image or on a
pre-setup laptop, there are two suggested modes of installation:

1) For a minimal installation to a disk image:

       ansible-pull -i localhost, -U https://github.com/ASPP/installation setup-ansible.yml

    After the disk image has been copied to a laptop, it is suggested to mount
    the root folder and manually enable the ansible timers. After a reboot, the
    system should then auto-install.

2) For a full installation:

       ansible-pull -i localhost, -U https://github.com/ASPP/installation all.yml

## Tags

Using

    ansible-playbook --list-tags all.yml

or

    ansible-playbook --list-tasks all.yml

it is possible to show the list of currently used tags.

Each task should have one of the following tags:

    - packages
    - graphical-packages
    - config
    - user-creation
    - user-packages
    - user-config

If in doubt, the playbook should be run untagged, but when only minor additions
are made to the playbook, specifying a tag may speed things up.


Furthermore, the individual stages have also been tagged:

    - stage-basic
    - stage-user
    - stage-bonus

## Troubleshooting

If connecting to the GitHub repo somehow does not work, it is possible to use
the fallback repo that was created in /root/installation at image creation
time.

    cd /root/installation
    ansible-playbook -i localhost, --connection local all.yml

