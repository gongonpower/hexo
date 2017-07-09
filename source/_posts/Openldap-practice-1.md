---
title: Openldap practice 1
date: 2017-07-09 18:03:02
tags:
---
# Modify rootdn
create-rootdn.ldif
```
changeType: modify
replace: olcSuffix
olcSuffix: dc=olimpus,dc=com
-
replace: olcRootDN
olcRootDN: cn=admin,dc=olimpus,dc=com
```
command:
```
ldapmodify -Y EXTERNAL -H ldapi:/// -f create-rootdn.ldif  
```
# Modify rootdn password
change-rootdn-password.ldif
```
dn: olcDatabase={2}bdb,cn=config
changeType: modify
replace: olcRootPW
olcRootPW: {SSHA}tHlbnWzxSSXwa06wgez05ODqtmVfQZYH
```
command:
```
ldapmodify -Y EXTERNAL -H ldapi:/// -f change-rootdn-password.ldif
```



