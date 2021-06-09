Role Name
=========
nar_solidfire_sds_uninstall 

Description
-----------
This role stops solidfire service, removes the sds package and configuration directories on hosts.
We recommend this role only be run on hosts not in an active cluster, and reachable via the network.
The same inventory file that was used for install can be used to uninstall the hosts.

WARNING: Uninstalling hosts from an active cluster can lead to data loss. All hosts in the supplied inventory file will be uninstalled.
Role should only be used during testing phase, not after deployment phase, for data safety.

Requirements
------------
This role requires the target systems use RHEL 7.6+ Additionally the target system is required to have solidfire sds installed.

Role Variables
--------------


| Variable                           | Required | Default  | Description                                 | Comments                               |
|------------------------------------|----------|----------|---------------------------------------------|----------------------------------------|
| sf_cluster_admin_passwd            | yes      | N/A      | The password for the Cluster Administrator  |                                        |
| sf_cluster_admin_username          | yes      | N/A      | The username for the Cluster Administrator  |                                        |
| sf_validate_certs                  | no       | True     | Check SSL/TLS certificates                  |                                        |
| sf_use_proxy                       | no       | False    | Use proxy config. See note [1] below                         |                                        |
| sf_api_version                     | no       | 12.2     | The version of the SolidFire eSDS API to    |                                        |
|                                    |          |          | use and should not be modified!             |                                        |
| sf_allow_uninstall_active_cluster  | no       | False    | True will allow uninstallation when the     |                                        |
|                                    |          |          | cluster is active which may cause data loss.|                                        |
|                                    |          |          | Nodes should be removed from active cluster |                                        |
|                                    |          |          | before running this role for data safety.   |                                        |

Notes:

[1] Setting sf_use_proxy may have no effect due to a bug in Ansible version 2.9.x or older. Instead, better to use
    the environment variable "no_proxy" in a playbook as a workaround when needed until the bug is fixed by Ansible. E.g.,
```ansible
    environment:
      no_proxy: <target_ip_address>                                                             
```

Example Playbook
----------------

```
  - name: Uninstall SolidFire Enterprise SDS
    hosts: all
    gather_facts: True

    roles:
      - role: nar_solidfire_sds_uninstall
```

License
-------

GNU v3

Author Information
------------------
NetApp
http://www.netapp.io
