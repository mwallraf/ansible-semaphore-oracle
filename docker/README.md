# Description

Customized dockerfile for semaphore that includes the OracleClient and python cx-Oracle library


# Build

docker build . --tag mwallraf/ansiblesemaphore-oracle:1.0

docker push mwallraf/ansiblesemaphore-oracle:1.0



# Ansible test playbook
This ansible playbook uses the collection ```ari_stark.ansible_oracle_modules``` for connecting to Oracle

```yaml
---
- name: oracle test
  hosts: localhost
  gather_facts: no
  collections:
    - ari_stark.ansible_oracle_modules

  tasks:

  - ari_stark.ansible_oracle_modules.oracle_sql:
      hostname: "172.21.212.105"
      username: "bo_read"
      password: "pui62wd3"
      service_name: "FTXPROD"
      sql: "select * from ftxuser.ISP"
```



# Python test script

```python
import cx_Oracle

hostname = "<yourip>"
port = "1521"
service = "<service>"
user = "<user>"
pwd = "<password>"

dsn_tns = cx_Oracle.makedsn(hostname, port, service_name=service)
conn = cx_Oracle.connect(user=user, password=pwd, dsn=dsn_tns)
```
