openshift-ipsec
===============

An Ansible role for configuring ipsec to secure communications between nodes
of an OpenShift cluster.
Role supports Opportunistic & Non-Opportunistic setups

Installation
------------

```
ansible-galaxy install https://github.com/jkupferer/ansible-role-openshift-ipsec/archive/master.tar.gz#/openshift-ipsec
```

Requirements
------------

An OpenShift cluster with an Ansible hosts file describing all cluster nodes as well as the additional variable
`ipsec_configuration` to control if Opportunistic IPSec should be used or Non-Oppoortunistic IPSec should be used.
For example:
Non-Opportunistic setup
```
ipsec_configuration = nonopportunistic
```
Opportunistic setup
```
ipsec_configuration = opportunistic
```

All nodes within the cluster need to allow IPSec related network traffic. This
includes IP protocol numbers 50 and 51 as well as UDP port 500.

IPSec also uses UDP port 4500 for NAT traversal, though this should not apply to normal cluster deployments.

The this role runs a task for `firewalld` as this should be the default with OCP >= 3.7, otherwise the below IPtables
example should be used.

For example, if the cluster nodes communicate over interface eth0, rules of
the following form may be added to `/etc/sysconfig/iptables`:

    -A OS_FIREWALL_ALLOW -i eth0 -p 50 -j ACCEPT
    -A OS_FIREWALL_ALLOW -i eth0 -p 51 -j ACCEPT
    -A OS_FIREWALL_ALLOW -i eth0 -p udp --dport 500 -j ACCEPT


Role Variables
--------------

* `ipsec_ca_dir` - Directory to store ipsec CA on masters (Default: `/etc/ipsec-ca`)

* `ipsec_ca_countryName` - Default country name value for certificates (Optional)

* `ipsec_ca_stateOrProvinceName` - Default state or province value for certificates (Optional)

* `ipsec_ca_localityName` - Default locality value for certificates (Optional)

* `ipsec_ca_organizationName` - Default organization value for certificates (Optional)

* `ipsec_ca_emailAddress` - Default email address value for certificates (Optional)

* `ipsec_ca_key` - CA key if one should not be auto-generated (Optional)

* `ipsec_ca_cert` - CA cert if one should not be auto-generated (Optional)


Example Playbook
----------------

    - hosts: nodes
      roles:
      - role: openshift-ipsec
        ipsec_ca_dir: /etc/ipsec-ca
        ipsec_ca_key: ca-key.pem
        ipsec_ca_cert: ca-crt.pem

License
-------

BSD

Author Information
------------------

Johnathan Kupferer (jkupfere@redhat.com)
Freddy Montero (fmontero@redhat.com)
