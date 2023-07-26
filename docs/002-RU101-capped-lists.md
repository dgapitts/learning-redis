## Week 002 - RU101 - capped-lists

To create a capped list that never grows beyond 100 elements, you can call LTRIM after each call to LPUSH:

```
> LPUSH notifications:user:1 "You've got mail!"
(integer) 1
> LTRIM notifications:user:1 0 99
OK
> LPUSH notifications:user:1 "Your package will be delivered at 12:01 today."
(integer) 2
> LTRIM notifications:user:1 0 99
```

and experimenting a little

```
127.0.0.1:6379> LPUSH notifications:user:1 "You've got mail!"
(integer) 1
127.0.0.1:6379> LTRIM notifications:user:1 0 9
OK
127.0.0.1:6379>
127.0.0.1:6379> LPUSH notifications:user:1 TIME
(integer) 2
127.0.0.1:6379> LPUSH notifications:user:1 TIME
(integer) 3
...
(integer) 12
127.0.0.1:6379> LPUSH notifications:user:1 TIME
(integer) 13
127.0.0.1:6379> LPUSH notifications:user:1 TIME
(integer) 14
127.0.0.1:6379> LPUSH notifications:user:1 TIME
(integer) 15
127.0.0.1:6379> LLEN notifications:user:1
(integer) 15
127.0.0.1:6379> LTRIM notifications:user:1 0 9
OK
127.0.0.1:6379> LLEN notifications:user:1
(integer) 10
```

and checking 
```
127.0.0.1:6379> LRANGE   notifications:user:1 0 20
 1) "TIME"
 2) "TIME"
 3) "TIME"
 4) "TIME"
 5) "TIME"
 6) "TIME"
 7) "TIME"
 8) "TIME"
 9) "TIME"
10) "TIME"
```


Although the TIME didn´t work as expected https://redis.io/commands/time/ ?


```
127.0.0.1:6379> TIMe
1) "1690374967"
2) "753387"
```

and finally a few more tests

```
127.0.0.1:6379> LRANGE notifications:user:2 0 20
(empty array)
127.0.0.1:6379> LTRIM notifications:user:1 0 3
OK
127.0.0.1:6379> LLEN notifications:user:1
(integer) 4
127.0.0.1:6379> LTRIM notifications:user:1 2 3
OK
127.0.0.1:6379>
127.0.0.1:6379> LLEN notifications:user:1
(integer) 2
```