---
title: Openldap practice 1
date: 2017-07-09 18:03:02
tags:
---
# Openldap slapd install
```
yum install -y openldap openldap-servers openldap-clients
service slapd start # centos 6
```
# Create ssha password
```
slappasswd
```
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
# Modify rootdn monitor auth
change-rootdn-monitor-auth.ldif
```
dn: olcDatabase={1}monitor,cn=config
changeType: modify
replace: olcAccess
olcAccess: {0}to * by dn.base="gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth" read by dn.base="cn=admin,dc=olimpus,dc=com" read by * none
```
command:
```
ldapmodify -Y EXTERNAL -H ldapi:/// -f change-rootdn-monitor-auth.ldif
```
# Add base organization
create-root-organization
```
dn: dc=olimpus,dc=com
objectClass: dcObject
objectClass: organization
dc: olimpus
o: olimpus
```
command:
```
ldapadd -f create-root-ou.ldif -D cn=admin,dc=olimpus,dc=com -W
```
# Add users ou
create-users-ou.ldif
```
dn: ou=users,dc=olimpus,dc=com
objectClass: organizationalUnit
ou: users
```
command:
```
ldapadd -f create-users-ou.ldif -D cn=admin,dc=olimpus,dc=com -W
```
# Add a user
create-a-user.ldif
```
dn: cn=Archimedes of Syracuse,ou=users,dc=olimpus,dc=com
cn: Archimedes
sn: Syracuse
objectClass: inetOrgPerson
userPassword: password
uid: archimedes
```
command:
```
ldapadd -f create-a-user.ldif -x -D cn=admin,dc=olimpus,dc=com -W
```
# Add a group
create-scientists-group.ldif
```
dn: cn=scientists,ou=users,dc=olimpus,dc=com
cn: scientists
objectClass: groupOfNames
member: cn=Aarchimedes of Syracuse,ou=users,dc=olimpus,dc=com
```
command:
```
ldapadd -f create-scientists-group.ldif -D cn=admin,dc=olimpus,dc=com -W
```
# Delete an entry
command:
```
ldapdelete "cn=Archimedes of Syracuse,ou=users,dc=olimpus,dc=com" -D cn=admin,dc=olimpus,dc=com -W
```

# Search command example
command:
```
ldapsearch -Y EXTERNAL -H ldapi:/// -b cn=config olcDatabase=\*
ldapsearch -Y EXTERNAL -H ldapi:/// -b cn=config olcAccess=\*
ldapsearch -x -b dc=olimpus,dc=com
```





