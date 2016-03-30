#### psoptphpcode
#####1
######xhprof
compile:
```
phpize
```
#####choose web server
######nginx apache
apache: apache2.4 php-fpm mpm_event

######config
```
sendfile on;  //optimize for static file
tcp_nopush on; //send complete package instead small packages
tcp_nodelay on;
keepalive_timeout 50;

```
access_log /var/log/access.log combined buffer=64k flush=5m  //how much content should be buffered before writing to file, if hasnot hit buffersize in 5 min, still save
gzip_min_length 1000
```

#####database opti
######mysql config (use percona)
```
show variables like "%version%";
/etc/mysql/my.cnf
```
######slowquery
```
/etc/mysql/my.cnf
```
show slow query log
```
select * from mysql.slow_log
```
edit
```
log_output='TABLE'

slow_query_log=1
slow_query_log_always_write_time=1
long_query_time=1
log_slow_verbosity='full'
slow_query_log_use_global_control='log_slow_verbosity,long_query_time'
```
######query optimization
```
insert into tbname(f1,f2) vaules('str',1) on duplicate key update f1=f1;
```
######denormalization
```
alter table a add column tb1f3 varchar(100);

update table join table2 on tb1f1=tb2f1 set tb1f3 = tb2f3
```
#####performance testing
######siege
```
./configure
make
make install
```
20 user
```
siege -c 20 --time=10S http://
```
