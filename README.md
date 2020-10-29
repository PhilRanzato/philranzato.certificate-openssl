plrr.certificate-openssl
=========

Create a CA or a Certificate with OpenSSL.

Requirements
------------

None.

Role Variables
--------------

```yaml
---
# Control variable to choose whether generating a ca or a certificate (or both)
generate: 
  ca: false
  certificate: false

# CA variables
ca:
  directory: /opt/private/ssl
  cert_name: "elastic"
  # cert_format: "crt | pem"
  cert_format: "crt"
  key_passphrase: "El4stic!"
  validity: "+80000d"
  size: "4096"
  type: "RSA"
  backup: yes
  country: "ES"
  organization: "elk"
  email: "elastic.kibana@logstash.elk"
  common_name: "ElkStack"
  # Values must be prefixed by their options. (i.e., email, URI, DNS, RID, IP, dirName, otherName and the ones specific to your CA)
  sans: "DNS:*.elk.es"
  basic_constraints:
  - "CA:TRUE"
  key_usage:
  - digitalSignature
  - keyAgreement
  owner: "root"
  group: "root"

# Certificates variables
certificate:
  from_ca:
    cert: /opt/private/ssl/elastic.crt
    key: /opt/private/ssl/elastic.key
    pass: "El4stic!"
  directory: /opt/private/ssl
  cert_name: "kibana"
  # cert_format: "crt | pem"
  cert_format: "crt"
  key_passphrase: "K1bana!"
  validity: "+3650d"
  size: "4096"
  type: "RSA"
  backup: yes
  country: "ES"
  organization: "elk"
  email: "elastic.kibana@logstash.elk"
  common_name: "ElkStack"
  # Values must be prefixed by their options. (i.e., email, URI, DNS, RID, IP, dirName, otherName and the ones specific to your CA)
  sans: 
  - "DNS:*.elk.es"
  - "IP:35.228.156.50"
  owner: "root"
  group: "root"
```

Dependencies
------------

- `python-pip` ~ installed by the role
- `cryptoghraphy` ~ installed by the role

Example Playbook
----------------

```yaml
- name: "Create Certificate"
  hosts: target
  roles:
  - { role: plrr.certificate-openssl }
  vars:
    generate: 
        ca: false
        certificate: false
    certificate:
        from_ca:
            cert: /opt/private/ssl/elastic.crt
            key: /opt/private/ssl/elastic.key
            pass: "El4stic!"
        directory: /opt/private/ssl
        cert_name: "kibana"
        # cert_format: "crt | pem"
        cert_format: "crt"
        key_passphrase: "K1bana!"
        validity: "+3650d"
        size: "4096"
        type: "RSA"
        backup: yes
        country: "ES"
        organization: "elk"
        email: "elastic.kibana@logstash.elk"
        common_name: "ElkStack"
        # Values must be prefixed by their options. (i.e., email, URI, DNS, RID, IP, dirName, otherName and the ones specific to your CA)
        sans: 
        - "DNS:*.elk.es"
        - "IP:35.228.156.50"
        owner: "root"
        group: "root"
```

License
-------

Proprietary

Author Information
------------------

Check me on [LinkedIn](www.linkedin.com/in/phil-ranzato-47b8bb194)
