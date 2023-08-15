### Setup via brew

```
    8  brew install redis
    9  redis-cli
   10  brew services start redis
   11  redis-cli
   12  brew services restart redis
```
### Download, unpack and add 

```
~/projects/learning-redis $ redis-cli
127.0.0.1:6379> CONFIG get dir
1) "dir"
2) "/usr/local/var/db/redis"
```

and download, unpack and add 

```
~ $ ls -l /usr/local/var/db/redis
total 3328
-rw-r--r--  1 dave  admin       89 Jul 23 18:20 dump.rdb
-rw-r--r--  1 dave  admin  1699740 Jul 24 00:19 ru101.rdb
```

### Download, unpack and add 


```
~ $ grep ^dbfilename /usr/local/etc/redis.conf
dbfilename dump.rdb
dbfilename ru101.rdb
```

### Simple check

```
~/projects/learning-redis $ redis-cli -h localhost -p 6379
localhost:6379> INFO keyspace
# Keyspace
db0:keys=14328,expires=0,avg_ttl=0
localhost:6379> dbsize
(integer) 14328
```
