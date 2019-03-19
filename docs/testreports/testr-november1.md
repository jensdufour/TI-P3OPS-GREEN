# Testplan November1

### Auteur(s): 
- Lennert Mertens- Maximilian Leire

## Alle te testen onderdelen onderverdeeld in secties:
### Test 1: Opzetten vm
- [x] open de commandline in de juiste repository map

- [x] vm opstarten 
```
$ vagrant up november1
```

- [x] vm provisionen zodat alle tasks worden uitgevoerd
```
$ vagrant provision november1
```
- [x] inloggen in de vm
```
$ vagrant ssh november1
```

### Test 2: Basisconfiguratie

- [x] ip adres is correct: `ip a`

- verwachte waarde :
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:8b:c9:3f brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global noprefixroute dynamic eth0
       valid_lft 82677sec preferred_lft 82677sec
    inet6 fe80::f291:687e:b2d4:4da0/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 08:00:27:6b:18:b9 brd ff:ff:ff:ff:ff:ff
    inet 172.16.0.37/24 brd 172.16.0.255 scope global noprefixroute eth1
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe6b:18b9/64 scope link
       valid_lft forever preferred_lft forever
```
- [x] default gateway is goed in gesteld `$ ip r`

verwachte waarde:
```
default via 10.0.2.2 dev eth0 proto dhcp metric 100
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15 metric 100
172.16.0.0/24 dev eth1 proto kernel scope link src 172.16.0.37 metric 101
```
- [x] mariadb service is running `$ systemctl status mariadb`

verwachte waarde:
```
● mariadb.service - MariaDB 10.3.10 database server
   Loaded: loaded (/usr/lib/systemd/system/mariadb.service; enabled; vendor preset: disabled)
  Drop-In: /etc/systemd/system/mariadb.service.d
           └─migrated-from-my.cnf-settings.conf
   Active: active (running) since Sun 2018-11-18 18:50:28 UTC; 52min ago
     Docs: man:mysqld(8)
           https://mariadb.com/kb/en/library/systemd/
  Process: 14922 ExecStartPost=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/SUCCESS)
  Process: 14752 ExecStartPre=/bin/sh -c [ ! -e /usr/bin/galera_recovery ] && VAR= ||   VAR=`/usr/bin/galera_recovery`; [ $? -eq 0 ]   && systemctl set-environment _WSREP_START_POSITION=$VAR || exit 1 (code=exited, status=0/SUCCESS)
  Process: 14750 ExecStartPre=/bin/sh -c systemctl unset-environment _WSREP_START_POSITION (code=exited, status=0/SUCCESS)
 Main PID: 14890 (mysqld)
   Status: "Taking your SQL requests now..."
   CGroup: /system.slice/mariadb.service
           └─14890 /usr/sbin/mysqld
```
### Test 3: echo1 database
- [x] inloggen met administratorrechten `$ mysql -uroot -pnovember1`

verwachte waarde:
```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 14
Server version: 10.3.10-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```
- [x] database echo1 bestaat `MariaDB [(none)]>  use dp_echo1`
- verwachte waarde:
```
Database changed
```

- [x] tables zijn leeg voor het aanmaken van de website `$ MariaDB [dp_echo1]> show tables;`
verwachte waarde: 
```
Empty set (0.000 sec)
```
- [x] website kan gelaunched worden
   - in webbrowser 172.16.0.7/drupal7/install.php intypen

#### 22/11/2018 Vervolg testing november1

- [x] drupal instalatie volgen en registreren (minimal is het gemakkelijkst)

- [x] kijken of connectie goed verloopt en tabbelen zijn opgevuld
  $ MariaDB [dp_echo1]> show tables;
  verwachte waarde: 
```
+----------------------------+
| Tables_in_dp_echo1         |
+----------------------------+
| drup_actions               |
| drup_authmap               |
| drup_batch                 |
| drup_block                 |
| drup_block_custom          |
| drup_block_node_type       |
| drup_block_role            |
| drup_blocked_ips           |
| drup_cache                 |
| drup_cache_block           |
| drup_cache_bootstrap       |
| drup_cache_field           |
| drup_cache_filter          |
| drup_cache_form            |
| drup_cache_menu            |
| drup_cache_page            |
| drup_cache_path            |
| drup_date_format_locale    |
| drup_date_format_type      |
| drup_date_formats          |
| drup_field_config          |
| drup_field_config_instance |
| drup_file_managed          |
| drup_file_usage            |
| drup_filter                |
| drup_filter_format         |
| drup_flood                 |
| drup_history               |
| drup_menu_links            |
| drup_menu_router           |
| drup_node                  |
| drup_node_access           |
| drup_node_revision         |
| drup_node_type             |
| drup_queue                 |
| drup_registry              |
| drup_registry_file         |
| drup_role                  |
| drup_role_permission       |
| drup_semaphore             |
| drup_sequences             |
| drup_sessions              |
| drup_system                |
| drup_url_alias             |
| drup_users                 |
| drup_users_roles           |
| drup_variable              |
| drup_watchdog              |
+----------------------------+
48 rows in set (0.000 sec)
```
### Test 4: mike1 database
- [x] inloggen met administratorrechten `$ mysql -uroot -pnovember1`

- verwachte waarde:
```
Welcome to the MariaDB monitor.  Commands end with ; or \g.
Your MariaDB connection id is 14
Server version: 10.3.10-MariaDB MariaDB Server

Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
```
- [x] database mike1 bestaat
  MariaDB [(none)]>  use wp_mike1
  verwachte waarde:
```
Database changed
```
- [x0] tables zijn leeg voor het aanmaken van de website
  $ MariaDB [wp_mike1]> show tables;
  verwachte waarde: 
```
Empty set (0.000 sec)
```
- [x] website kan gelaunched worden: in webbrowser 172.16.0.36/wordpress intypen

- [x] wordpress account aanmaken en wordpress installeren

- [x] kijken of connectie goed verloopt en tabbelen zijn opgevuld
  $ MariaDB [wp_mike1]> show tables;
  verwachte waarde:
```
+-----------------------+
| Tables_in_wp_mike1    |
+-----------------------+
| wp_commentmeta        |
| wp_comments           |
| wp_links              |
| wp_options            |
| wp_postmeta           |
| wp_posts              |
| wp_term_relationships |
| wp_term_taxonomy      |
| wp_termmeta           |
| wp_terms              |
| wp_usermeta           |
| wp_users              |
+-----------------------+
12 rows in set (0.001 sec)
```

- Testen volgens testplan allemaal geslaagd.#### 10/12/2018 Testen op fysieke servers (Max L.)- In orde