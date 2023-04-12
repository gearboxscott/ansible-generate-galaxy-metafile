ansible-generate-galaxy-metafile
=========

This playbook will generate a meta.yml file that can be use as a role's `meta/main.yml` file. Preset variables in the `inventory.yml` like `author`, `platforms`, `dependencies`, etc.

Requirements
------------

It recommended that occasionally run the `pull_current_platforms.yml` playbook to get a list of current supported platform in `https://galaxy.ansible.com` to set the `platforms_search` variable to the supported platforms for your role.

```bash
ansible-playbook -i inventory.yml pull_current_platforms.yml > platforms.txt
```

Lastly, change the variables in `inventory.yml` to set information for the role that the galaxy meta file is being created.

> NOTE: Create a inventory file for each role like `role-lnx-update-inventory.yml` for example.

Variables
--------------

The following table is variables that can be set for your galaxy metafile for each of your roles:

| Variable | Type | Required | Defaults | Comments |
|-|:-:|:-:|-|-|
| `author` | string | Y | None | Your name |
| `description` | string | Y | None | Your role description |
| `company` | string | N | Null | Your company |
| `min_ansible_container_version` | float | N | Null | If this a Container Enabled role, provide the minimum Ansible Container version |
| `issue_tracker_url` | string | Y | Null | If the issue tracker for your role is not on github, uncomment the next line and provide a value |
| `license` | string | N | `license (GPL-2.0-or-later, MIT, etc)` | Choose a valid license ID from https://spdx.org - some suggested licenses: BSD-3-Clause (default), MIT,  GPL-2.0-or-later, GPL-3.0-only, Apache-2.0, CC-BY-4.0 |
| `min_ansible_version` | float | Y | `2.9` | Minimum version of Ansible that supports your role |
| `galaxy_tags` | dictionary | N | None | List tags for your role here, one per line. A tag is a keyword that describes and categorizes the role. Users find roles by searching for tags. Be sure to remove the '[]' above, if you add tags to this list. NOTE: A tag is limited to a single word comprised of alphanumeric characters.  Maximum 20 tags per role. |
| `dependencies` | dictionary | N | None | List your role dependencies here, one per line. |
| `platforms_search` | dictionary | N | None | Search for the platforms that support your role available on `https://galaxy.ansible.com`. After the meta file is generate it will contain the platform and version of that platform. Remove the versions that are not relevant to your role |

Of the time of this document was written the following are validate platforms for this role:

| Platform | Platform | Platform | Platform | Platform |
|:-:|:-:|:-:|:-:|:-:|
| AIX | Alpine | Amazon | Amazon Linux 2 | aos |
| ArchLinux | ClearLinux | Cumulus | Debian | DellOS
| Devuan | DragonFlyBSD | EL | eos | Fedora
| FreeBSD | GenericBSD | GenericLinux | GenericUNIX | Gentoo
| HardenedBSD | IOS | Junos | macOS | MacOSX
| NXOS | OpenBSD | opensuse | os10 | PAN-OS |
| SLES | SmartOS | Solaris | Synology | TMOS |
| Ubuntu | vCenter | Void Linux | vSphere | Windows |

The following is an example of an inventory file for running creating a sample meta file:

```yaml
---

all:
  hosts:
    localhost:
      ansible_connection: local
  vars:
    author: Nickoli Tesla
    description: "This role will do something, don't know what but it will do something"
    company: Static Electricity Company
    destination: ./meta.yml
    platforms_search:
      - EL
      - fedora
      - opensuse
      - SLES

...

```

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Project Playbook
----------------

The following is an example of how to use your role:

```yaml
---
- name: Display a list of platform for Galaxy Meta File
  hosts: localhost
  gather_facts: true
  roles:
    - role: 'roles/role_generate_metafile'

...

```

License
-------

GPL

Author Information
------------------

Scott Parker - Red Hat Consulting - NA - sparker@redhat.com