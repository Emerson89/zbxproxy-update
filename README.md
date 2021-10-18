## Update version zabbix-server using ansible for 5.0 >

![Badge](https://img.shields.io/badge/ansible-zabbix-red)

## Dependencies
![Badge](https://img.shields.io/badge/ansible-2.9.10-blue)

## Testados em SO 
- Centos 7 somente suporte até o 5.0
- Rocky 8
- Ubuntu 18
- Ubuntu 20

## Importante 

Realize o dump do banco

## Edit the inventory file 
Ex:
```
[zabbix]
xx.xxx.xxx.xx 
```
## Playbook example
```
---
- name: Update Zabbix-server
  hosts: all
  vars:
    zbx_database_password: INSIRA-AQUI-SUA-SENHA-BANCO
    zabbix_version: 5.0 <= DEFAULT PARA CENTOS 7 SUPORTE VERSÃO FINAL
  become: yes
  roles:
  - zbx-server
  - zbx-front
```
``` 
ansible-playbook -i hosts playbook.yml
``` 
## ATTENTION: 

1- the backup of the old zabbix will be stored in the directory /tmp/zabbix-backup

2 - Check the version of mysql for 5.6 you will need to update to one above this one was tested in version 5.7.33, tested in version 5.6 will present the error of type:
```
zabbix | 7:20200525:040444.998 starting automatic database upgrade
zabbix | 7:20200525:040444.998 [Z3005] query failed: [1071] Specified key was too long; max key length is 3072 bytes [create index items_1 on items (hostid,key_(1021))]
zabbix | 7:20200525:040444.998 database upgrade failed
```
3- To update the mysql version
```
rm -rf /etc/yum.repos.d/RepoMYSQL.repo - remove repo antigo 
systemctl stop mysqld - pare o serviço
yum install https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm - install repo
yum update mysql-community-server -y - update version
mysql --version - verifica version
systemctl start mysqld - start service
systemctl status zabbix-server - status do server 
tail -f /var/log/zabbix/zabbix_server.log
```

IN PRODUCTION CAREFULLY EXECUTE ANY CHANGE IN THE BANK AND ALWAYS BACKUP

## License
![Badge](https://img.shields.io/badge/license-GPLv3-green)
