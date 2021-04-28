selfsigned_demo_ca
=========

Setup a selfsigned demo CA (certificate authority) and generate certificates for hosts. In the latter case, the host's FQDN will be used as the `common name` for the certificate.

Requirements
------------

None. The prerequisites that the Ansible `openssl_*` modules need on the target hosts will be installed automatically.

Role Variables
--------------

All default variables are called `default_X`, and will automatically be used to fill the actually used variables called `X`, if those are not yet defined.
*Example*:
`default_ca_common_name` => `ca_common_name`
The value in `default_ca_common_name` will be used as value for `ca_common_name`, if it is not defined yet.

So, you can override all variables by just setting the variables without the `default_` prefix.

There are some variables that do not have a default, obviously:

- `ca_key_passphrase`: passphrase to be used for the CA's private key

There are two variables that control what the role does, whether it creates the Demo CA or whether it creates host certificates:
- `generate_demo_ca`: set this to `true` if you want the role to create the Demo CA
- `create_certs_for_hosts`: set this to `true` if you want the role to create host certificates

The variables that have a default are the following:

# Default folders
- `ca_target_folder`: the folder to store the CA certificate, default ist `/etc/pki/tls/private/`
- `host_certs_target_folder`: the folder on the target host where to store the host's certificate, default is `/etc/pki/tls/private/`

# permission settings for the host certificates
- `certs_file_user`: user that will own the certificate files, default is `root`
- `certs_file_group`: group that will own the certificate files, default is `root`
- `certs_file_mode`: permissions for the certificate file, default is `0644`
- `certs_key_file_mode`: permissions for the key file, default is `0600`
- `certs_directory_mode`: permissions for the certificate directory, default is `0700`

# ca settings
- `ca_common_name`: common name used for the CA certificate, default is `B1 Training Demo CA`
- `ca_organization_name`: organization used for the CA certificate, default is `B1 Systems GmbH`
- `ca_organizational_unit_name`:  organizational unit used for the CA certificate, default is `B1 Training`
- `ca_country_name`:  country name used for the CA certificate, default is `DE`
- `ca_state_or_province_name`:  state or province used for the CA certificate, default is `Bavaria`
- `ca_locality_name`:  locality used for the CA certificate, default is `Rockolding`
- `ca_key_type`:  key type used for the CA certificate key, default is `RSA`
- `ca_key_cipher`: key cipher used for the CA certificate key, default is `auto` (as recommended by the [Ansible module documentation](https://docs.ansible.com/ansible/latest/collections/community/crypto/openssl_privatekey_module.html))
- `ca_key_size`: key size used for the CA certificate key, default is `4096`
- `ca_key_file`: file name for the CA key, default is `b1training_democa.key`
- `ca_crt_file`: file name for the CA certificate, default is `b1training_democa.crt`
- `ca_csr_file`: file name for the CA CSR, default is `b1training_democa.csr`

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
