Role Name
=========

Create a samba server

Requirements
------------

None

Role Variables
--------------

Variables for samba role


# defaults file for samba

# following variable should be secured in a vault
samba_userlist:
  username: ''
  password: ''

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
    force_group: "{{ samba_group }}"


  - name: backups
    comment: Backups
    share_path: /exp/cifs/backups
    mode: 2550
    conf_access_rights: "public = yes"
    conf_valid_users: "valid users = {{ samba_smb_group }}"
    create_mask: ""
    directory_mask: ""
    read_only: "read only = yes"
    force_group: "{{ samba_group }}"
    force_create_mode "force create mode = 0660"
  - name: public
    comment: Public
    share_path: /exp/cifs/data/public
    mode: 2550
    conf_access_rights: "public = yes"
    conf_valid_users: ""
    create_mask: ""
    directory_mask: ""
    read_only: "read only = yes"
    force_group: "{{ samba_group }}"
    force_create_mode "force create mode = 0660"

Dependencies
------------

None.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - name: samba-server

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

