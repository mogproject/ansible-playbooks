MySQL Replication
=================

Setup MySQL servers with replication


Worked with ...
----

- CentOS 6.5 x86_64
- Ansible 1.5.4
- MySQL 5.6.17
- Vagrant 1.4.2


How to Use
----

### with Vagrant

```
git clone https://github.com/mogproject/ansible-playbooks.git
cd ansible-playbooks/mysql-replication
vagrant up
```

If you want to provision again, try this.

```
vagrant provision
```

### Play with data

Create a table and insert one record to the ```awesome``` database on ```mysql-master```.

```
mysql -h 192.168.81.11 -u awesome awesome  # password is 'awesome'

mysql> create table person (id int, name varchar(20));
Query OK, 0 rows affected (0.11 sec)

mysql> insert into person (id, name) values (10, 'foobar');
Query OK, 1 row affected (0.02 sec)

mysql> select * from person;
+------+--------+
| id   | name   |
+------+--------+
|   10 | foobar |
+------+--------+
1 row in set (0.00 sec)

mysql> exit
```

Next, access to ```mysql-slave```.

```
mysql -h 192.168.81.12 -u awesome awesome  # password is 'awesome'

mysql> select * from person;
+------+--------+
| id   | name   |
+------+--------+
|   10 | foobar |
+------+--------+
1 row in set (0.00 sec)

mysql>
```

Awesome! Data is replicated.

