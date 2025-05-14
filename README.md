## Update version zabbix-proxy using ansible

![Badge](https://img.shields.io/badge/ansible-zabbix-red)

## Dependencies
![Badge](https://img.shields.io/badge/ansible-2.9.10-blue)

## Testado 
- ansible 2.9.6
- Testado no `Almalinux8` 
- Banco de dados Sqlite e Mysql

## Edit the inventory file 
Ex:
```
[zabbix]
xx.xxx.xxx.xx 
```
Variáveis
-----------------
| Nome | Descrição | Default | 
|------|-----------|---------|
| zabbix_version | Versão zabbix-server | 4.4|
| zabbix_proxy_database | Tipo de database[mysql/sqlite3] | sqlite3

## Importante

**Erro mysql** 

```
query failed: [1419] You do not have the SUPER privilege and binary logging is enabled (you *might* want to use the less safe log_bin_trust_function_creators variable)
```

Verifique se o usuário tem privilegio SUPER ou desabilite `log_bin_trust_function_creators = 1` em `my.cnf` antes da atualização

## Playbook example
```
---
- hosts: all
  vars:
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
