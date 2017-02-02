openshift-ipsec
===============

An Ansible role for configuring ipsec to secure communications between nodes
of an OpenShift cluster.

Installation
------------

```
ansible-galaxy install https://github.com/jkupferer/ansible-role-openshift-ipsec/archive/master.tar.gz#/openshift-ipsec
```

Requirements
------------

An OpenShift cluster with an Ansible hosts file describing all cluster nodes.

Role Variables
--------------

* `ipsec_ca_dir` - Directory to store ipsec CA on masters (Default: `/etc/ipsec-ca`)

* `ipsec_ca_countryName` - Default country name value for certificates (Optional)

* `ipsec_ca_stateOrProvinceName` - Default state or province value for certificates (Optional)

* `ipsec_ca_localityName` - Default locality value for certificates (Optional)

* `ipsec_ca_organizationName` - Default organization value for certificates (Optional)

* `ipsec_ca_emailAddress` - Default email address value for certificates (Optional)


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: nodes
      roles:
      - role: openshift-ipsec
        ipsec_ca_dir: /etc/ipsec-ca

License
-------

BSD

Author Information
------------------

Johnathan Kupferer (jkupfere@redhat.com)
