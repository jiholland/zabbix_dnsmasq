dnsmasq by zabbix agent
=======================

This [template](https://www.zabbix.com/documentation/current/en/manual/xml_export_import/templates#importing) monitors:
- dnsmasq service
- dnsmasq dhcp-scope

Add dnsmasq.conf to `/etc/zabbix/zabbix_agentd.d/` and ensure `/etc/zabbix/zabbix_agentd.conf` includes files from the directory:
```yaml
...
Include=/etc/zabbix/zabbix_agentd.d/*.conf
```
Make sure selinux is not blocking read access to `/etc/dnsmasq.conf` and `/var/lib/dnsmasq/dnsmasq.leases`
```yaml
$ sudo journalctl -t setroubleshoot
```
Create and install policies if selinux is preventing access. Example:
```yaml
$ sudo grep dnsmasq.conf /var/log/audit/audit.log | audit2allow -M zabbix_dnsmasq_conf_policy
$ sudo semodule -i zabbix_dnsmasq_conf_policy.pp
```
☕️ Jørn Ivar
