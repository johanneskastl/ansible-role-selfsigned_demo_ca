selfsigned_demo_ca
=========

Setup a selfsigned demo CA (certificate authority) and generate some certificates

Requirements
------------

None.

Role Variables
--------------

None.

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: 'johanneskastl.selfsigned_demo_ca' }

Example Playbook for creating a host certificate
----------------

    - hosts: servers
      roles:
        - role: 'johanneskastl.selfsigned_demo_ca'
          vars:
            ca_target_folder: 'B1_Training_demo_CA/'
            host_certs_target_folder: '/some/folder/'
            certs_file_user: 'ldap'
            certs_file_group: 'ldap'
            create_certs_for_hosts: 'true'
            # NOT FOR PRODUCTION, use ansible vault or similar
            ca_key_passphrase: 'somethingtotallysecret'

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
