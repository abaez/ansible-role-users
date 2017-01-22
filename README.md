ansible-role-user
=========
[![license][2i]][2p]
[![twitter][3i]][3p]

A small user creation for [docker], [sudo]  permission based provision.

Description
-----------

Provisions the client to follow the [archlinux][5]'s wiki on building a secure **sudo** environment. The role is initially builds a user with the group access to:

- ssh
- docker

With these groups, when run with the [sudo] role, you gain the abilities detailed on the [archlinux][5] sudo wiki guide. The normal use produced would only gain higher domain access through sudo to a system user. The normal user also does not have write access to anything on the system and is only used to manage the currently working setup of the containers running on the client through [docker]. This allows to keep the user from being compromised to a minimum.

At the same time, with the use of the [sshd] role, you also gain the ability of keeping the user limited to remote access only through the **RSA** key.

Role Variables
--------------

The role has two variable maps that need to be changed, both dealing with user creation:

``` yaml
user:
  name: lo # some user name to be the normal user.
  home: # the home for this user.
  pub: # the ssh  pubkey you want to use for access to user remotely.
```

All the home, pub, and user name need to be changed to accomadate the use of the role.

Requirements
------------

Does not need to have **docker** installed, but can be helpful in the process when adding the groups usage. It will create the **docker** group if the group does not exist on the client.

Usage
-----

You **need** the `.pub` key value, listed in *Role Variables* above, to gain access to the user.

The container also needs the `defaults/main.yml` variables of **super** and **main** changed as detailed on the description and *role variables*. Other than that, nothing else needs to be appended to be changed to run the role.

``` yaml
- hosts: servers
    roles:
        - abaez.user
```

Author Information
------------------

[Alejandro Baez][1]

[docker]: https://www.docker.com/

[1]: https://keybase.io/baez
[2i]: https://img.shields.io/badge/license-BSD_2-green.svg
[2p]: ./LICENSE
[3i]: https://img.shields.io/badge/twitter-a_baez-blue.svg
[3p]: https://twitter.com/a_baez
[5]: https://wiki.archlinux.org/index.php/Sudo#Harden_with_Sudo_Example

[sshd]: https://galaxy.ansible.com/abaez/sshd
[sudo]: https://galaxy.ansible.com/abaez/sudo
