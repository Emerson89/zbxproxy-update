## Update version zabbix-proxy using ansible

![Badge](https://img.shields.io/badge/ansible-zabbix-red)

## Dependencies
![Badge](https://img.shields.io/badge/ansible-2.9.10-blue)

## Testados em SO 
- ansible 2.9.6
- Suporte as distribuições baseadas em Debian e RedHat
- Testado no Ubuntu20, Rocky8 e Centos7 
- Banco de dados Sqlite e Mysql

## Edit the inventory file 
Ex:
```
[zabbix]
xx.xxx.xxx.xx 
```
Importante
-----------------
Existem 2 database_types que serão suportados: mysql e sqlite. Você precisará inserir as variáveis no playbook o banco de dados que deseja usar, caso contrário seguirá o default que é SQlite3 assim como outras variáveis.

## Playbook example
```
---
- hosts: all
  vars:
    zabbix_server_ip: IP-ZABBIX-SERVER
    zbx_database_password: PASSWORD-DB-ZABBIX
    zabbix_proxy_database: mysql or sqlite3
    zabbix_version: 4.4
  roles:
    - zbx-proxy
  become: yes
```
``` 
ansible-playbook -i hosts playbook.yml
``` 
## License
![Badge](https://img.shields.io/badge/license-GPLv3-green)
