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

Example Playbook for the creation of a Demo CA
----------------

    - name: 'Create a self-signed CA on localhost'
      hosts: 'localhost'
      gather_facts: 'yes'
      become: 'false'

      roles:
        - role: 'johanneskastl.selfsigned_demo_ca'
          vars:
            # this playbook creates the Demo CA, no certificates for hosts
            generate_demo_ca: 'true'
            create_certs_for_hosts: 'false'
            # Variables for the CA
            ca_key_file: 'b1training_democa.key'
            ca_crt_file: 'b1training_democa.crt'
            ca_target_folder: 'B1_Training_demo_CA/'
            # NOT FOR PRODUCTION, use ansible vault or similar
            ca_key_passphrase: 'somethingtotallysecret'

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
