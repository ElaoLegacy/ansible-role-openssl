# Ansible Role: OpenSSL

This role will install OpenSSL on the spedified hosts and manage SSL certificates. It's able to deal with "real" certificates and keys as autosigned custom certificates

It's part of the ELAO Ansible stack but can be used stand alone.

## Requirements

- Ansible 1.7.2+

## Dependencies

None.

## Installation

Using ansible galaxy:

```bash
ansible-galaxy install elao.openssl
```
You can add this role as a dependency for other roles by adding the role to the meta/main.yml file of your own role:

```yaml
dependencies:
  - { role: elao.openssl }
```

## Role Handlers

    None

## Role Variables

### Configuration example

```
---

elao_openssl_files_path:    /etc/ssl-elao
elao_openssl_keys_path:     "{{ elao_openssl_files_path }}/private"
elao_openssl_certs_path:    "{{ elao_openssl_files_path }}/certs"

elao_openssl_self_signed:
    global:
        common_name:        "*.mysite.local"        # This one is mandatory and can't be null
        state:              "Rhône-Alpes"
        locality_name:      LYON
        organization_name:  ELAO
        unit_name:          IT                      # Organization Unit Name
        email_address:      hosting@elao.com
        ttl:                365
        passphrase:         MyAwesomePassword

    pma:
        common_name:        "sql.mysite.local"      # This one is mandatory and can't be null
        country:            FR                      # Country Name
        state:              "Rhône-Alpes"
        locality_name:      LYON
        organization_name:  ELAO
        unit_name:          IT                      # Organization Unit Name
        email_address:      hosting@elao.com
        ttl:                365                     # Corresponding to the -days option
        passphrase:         MyAwesomePassword
```

## Example playbook

    - hosts: servers
      roles:
         - { role: elao.openssl }

# TODO
Allow to add signed certs from local repository

# Licence

MIT

# Author information

ELAO [**(http://www.elao.com/)**](http://www.elao.com)