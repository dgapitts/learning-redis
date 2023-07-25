## Introduction to Redis hashes

Redis hashes are record types structured as collections of field-value pairs. 
https://redis.io/docs/data-types/hashes/


### hset

```
localhost:6379> hset bike:1 model Deimos brand Ergonom type 'Enduro bikes' price 4972
(integer) 4
localhost:6379> dbsize
(integer) 14329
```

### hget

```
localhost:6379> hget bike:1 model
"Deimos"
localhost:6379> hget bike:1 price
"4972"
localhost:6379> hget bike:1
(error) ERR wrong number of arguments for 'hget' command
```

### hgetall

```
localhost:6379> hgetall bike:1
1) "model"
2) "Deimos"
3) "brand"
4) "Ergonom"
5) "type"
6) "Enduro bikes"
7) "price"
8) "4972"
```

### hmget

```
localhost:6379> hmget bike:1 model price no-such-field
1) "Deimos"
2) "4972"
3) (nil)
```


### hincrby

```
localhost:6379> hincrby bike:1 price 100
(integer) 5072
localhost:6379> hincrby bike:1 price -100
(integer) 4972
localhost:6379> hset hash-one a "abc"
(integer) 1
localhost:6379> hincrby hash-one b 10
(integer) 10
localhost:6379> hgetall hash-one
1) "a"
2) "abc"
3) "b"
4) "10"
```


