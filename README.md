# Ansible Role: Pure-FTPd

[![Build Status](https://travis-ci.org/tschifftner/ansible-role-pureftpd.svg)](https://travis-ci.org/tschifftner/ansible-role-pureftpd)

Installs Pure-FTPd on Debian/Ubuntu linux servers.

## Requirements

None.

## Role Variables

Available variables are listed below, along with other default values (see `defaults/main.yml`):

To create a ftp account define all account as follows:

```
pureftpd_users:
  - name: ftpuser
    password: '$2....40'
    home: '/var/www/site'
    uid: '1002'
    gid: '1002'

```

To allow virtual users, one single user will be created:
```
pureftpd_user: 'ftpuser'
pureftpd_group: 'ftp'
```

### Config Variables

Values should be surrounded by quotation marks as otherwise yes becomes True

```
pureftpd_config:
  ChrootEveryone:              'yes'
  BrokenClientsCompatibility:  'no'
  MaxClientsNumber:            '50'
  Daemonize:                   'yes'
  MaxClientsPerIP:             '{{ ansible_processor_cores }}'
  VerboseLog:                  'yes'
  DisplayDotFiles:             'yes'
  AnonymousOnly:               'no'
  NoAnonymous:                 'yes'
  SyslogFacility:              'ftp'
#  FortunesFile:                '/etc/pure-ftpd/cookie'
  DontResolve:                 'yes'
  MaxIdleTime:                 '15'
#  LDAPConfigFile:              /etc/pureftpd-ldap.conf
#  MySQLConfigFile:             /etc/pure-ftpd/mysql.conf
#  PGSQLConfigFile:             /etc/pureftpd-pgsql.conf
  PureDB:                       /etc/pure-ftpd/pureftpd.pdb
#  ExtAuth:                     /var/run/ftpd.sock
  PAMAuthentication:           'no'
#  UnixAuthentication:          'yes'
  LimitRecursion:              '10000 8'
  AnonymousCanCreateDirs:      'no'
#  MaxLoad:                     '4'
#  PassivePortRange:            '30000 50000'
#  ForcePassiveIP:              '192.168.0.1'
#  AnonymousRatio:              '1 10'
#  UserRatio:                   '1 10'
  AntiWarez:                   'yes'
#  Bind:                         '127.0.0.1,21'
#  AnonymousBandwidth:           '8'
#  UserBandwidth:                '8'
  Umask:                       '117 007'
#  MinUID:                      '2001'
  AllowUserFXP:                'no'
  AllowAnonymousFXP:           'no'
  ProhibitDotFilesWrite:       'no'
  ProhibitDotFilesRead:        'no'
  AutoRename:                  'no'
  AnonymousCantUpload:         'no'
#  TrustedIP:                   '10.1.1.1'
#  LogPID:                      'yes'
  AltLog:                      'clf:/var/log/pureftpd.log'
#  AltLog:                      'stats:/var/log/pureftpd.log'
#  AltLog:                      'w3c:/var/log/pureftpd.log'
  NoChmod:                     'yes'
  KeepAllFiles:                'yes'
  CreateHomeDir:               'yes'
#  Quota:                       '1000:10'
#  PIDFile:                     '/var/run/pure-ftpd.pid'
#  CallUploadScript:           'yes'
#  MaxDiskUsage:                '99'
#  NoRename:                    'yes'
  CustomerProof:               'yes'
#  PerUserLimits:               '3:20'
#  NoTruncate:                  'yes'
  TLS:                         '0'
  IPV4Only:                    'yes'
#  IPV6Only:                    'yes'
#  FileSystemCharset:           'utf8'
#  ClientCharset:               'cp1251'
```


## Dependencies

None.

## Example Playbook

    - hosts: server
      roles:
        - { role: tschifftner.pureftpd }

## License

MIT / BSD

## Author Information

 - Tobias Schifftner, @tschifftner