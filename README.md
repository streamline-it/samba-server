Role Name
=========

A brief description of the role goes here.

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
Variables for samba role


# defaults file for samba
# user group used for the directory structure for Discretionary Access Control
samba_smb_group: smbusers
# This user will exist on the host and can be used to mount the samba share to the client
samba_smb_smbuser: smbuser
# smb.conf: NETBIOS name 
samba_netbios_name: server
# smb.conf: map to guest line
samba_maptoguest: "map to guest = bad user"
# smb.conf: interfaces to bind to
samba_interfaces: 127.0.0.1
# samba.conf: this apppends to hosts_allow
samba_client_list
# smb.conf: hosts to allow access
samba_hosts_allow: "127.0.0.1 {{ samba_client_list }}"
# smb.conf: workgroup name 
samba_workgroup: workgroup
# smb.conf: log file path
samba_log_file_path: /var/log/samba/log.smbd
# smb.conf: log level for samba logging
samba_log_level: 2
# smb.conf: samba log max file size
samba_log_max_size: 500

# smb.conf Service listing with options
samba_service_shares:
  - name: docs
    comment: Documents
    share_path: exp/cifs/data/docs
    mode: 2770
    conf_access_rights: "write_list = {{ samba_smb_group }}"
    conf_valid_users: "valid users = {{ samba_smb_group }}"
    create_mask: "create mask = 0660"
    directory_mask: "directory mask = 0770"
    read_only: "read only = no"
  - name: backups
    comment: Backups
    share_path: /exp/cifs/backups
    mode: 2550
    conf_access_rights: "public = yes"
    conf_valid_users: "valid users = {{ samba_smb_group }}"
    create_mask: ""
    directory_mask: ""
    read_only: "read only = yes"
  - name: public
    comment: Public
    share_path: /exp/cifs/data/public
    mode: 2550
    conf_access_rights: "public = yes"
    conf_valid_users: ""
    create_mask: ""
    directory_mask: ""
    read_only: "read only = yes"
