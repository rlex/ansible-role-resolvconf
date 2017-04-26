Simple role for configuring resolv.conf file  
Please note that resolvconf package will be removed (on debian/ubuntu) to persist this settings after reboots.  
By default, it will configure nameservers to Google DNS and Level3 DNS  

Example playbook:
```yml
- name: install resolvconf config
  hosts: all
  roles:
    - resolvconf
```

You can specify settings in group/host vars, for example:
```yml
resolvconf_domain: int.lan.platform
resolvconf_search:
  - int.lan.platform
  - lan.platform
resolvconf_sortlist: 10.0.0.0/255.0.0.0
resolvconf_options:
  - attempts:2
  - timeout:1
  - rotate
  - single-request-reopen
resolvconf_nameservers:
  - 8.8.8.8
  - 8.8.4.4
  - 209.244.0.3
  - 209.244.0.4
```

Will result in:
```
# Ansible managed: file modified on 2017-04-26 14:11:16
domain int.lan.home
search int.lan.platform lan.platform
nameserver 8.8.8.8
nameserver 8.8.4.4
nameserver 209.244.0.3
nameserver 209.244.0.4
sortlist 10.0.0.0/255.0.0.0
options attempts:2 timeout:1 rotate single-request-reopen
```

P.S. sortlist here is only for compatibility. It's not advised to use it today.  
Please refrain from using it and use [gai.conf](https://linux.die.net/man/5/gai.conf) instead
