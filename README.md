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

License
-------

BSD-3-Clause

Author Information
------------------

I am Johannes Kastl, reachable via kastl@b1-systems.de.
