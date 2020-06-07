# Hbase туториал
Вход в консоль:
```sh
hbase shell
```
Создание пространства имен **my_ns**:
```sh
hbase(main):013:0> create_namespace 'my_ns'
```
Просмотр всех пространств имен:
```
hbase(main):013:0> list_namespace
```
Просмотр таблиц в пространстве имен my_ns
```
hbase(main):013:0> list_namespace_tables 'my_ns'
```
Просмотр всех таблиц во всех пространствах имен
```
hbase(main):013:0> list
```
# Работа с таблицами
Создание таблицы в пространстве имен **my_ns**
```
hbase(main):013:0> create 'my_ns:test', 'cf'
```
Проверяем что есть таблица в нашем пространстве имен. К примеру так:
```
hbase(main):013:0> list 'my_ns:test'
TABLE                                                                           
my_ns:test                                                                      
1 row(s)
Took 0.0052 seconds 
```
Описание таблицы:
```
hbase(main):013:0>  describe 'my_ns:test'
able my_ns:test is ENABLED                                                     
my_ns:test                                                                      
COLUMN FAMILIES DESCRIPTION                                                     
{NAME => 'cf', VERSIONS => '1', EVICT_BLOCKS_ON_CLOSE => 'false', NEW_VERSION_BE
HAVIOR => 'false', KEEP_DELETED_CELLS => 'FALSE', CACHE_DATA_ON_WRITE => 'false'
, DATA_BLOCK_ENCODING => 'NONE', TTL => 'FOREVER', MIN_VERSIONS => '0', REPLICAT
ION_SCOPE => '0', BLOOMFILTER => 'ROW', CACHE_INDEX_ON_WRITE => 'false', IN_MEMO
RY => 'false', CACHE_BLOOMS_ON_WRITE => 'false', PREFETCH_BLOCKS_ON_OPEN => 'fal
se', COMPRESSION => 'NONE', BLOCKCACHE => 'true', BLOCKSIZE => '65536'}         
1 row(s)
Took 0.1379 seconds 
```
Вставка данных:
```
hbase(main):013:0> put 'my_ns:test', 'row1', 'cf:a', 'value1'
Took 0.2336 seconds 
hbase(main):013:0> put 'my_ns:test', 'row2', 'cf:b', 'value2'
Took 0.2536 seconds 
hbase(main):013:0> put 'my_ns:test', 'row3', 'cf:c', 'value3'
Took 0.2337 seconds 
```
Просмотрим 10 записей таблицы:
```
hbase(main):004:0> scan 'my_ns:test' ,{LIMIT => 10}
ROW                   COLUMN+CELL                                               
 row1                 column=cf:a, timestamp=1589421483984, value=value1        
 row2                 column=cf:b, timestamp=1589421652616, value=value2        
 row3                 column=cf:c, timestamp=1589421717676, value=value3        
3 row(s)
Took 0.0383 seconds
```
Получения данных по ключю:
```
base(main):005:0> get 'my_ns:test', 'row1'
COLUMN                CELL                                                      
 cf:a                 timestamp=1589421483984, value=value1                     
1 row(s)
Took 0.0556 seconds
```
Просморт количества строк. Расчет при уеличении  CACHE 
```
count 'my_ns:test', CACHE => 100000
```
Сделать не активную таблицу
```
disable 'my_ns:test'
```
Удалим таблицу
```
drop 'my_ns:test'
```

Рекомендации:
- Стараться хранить более мелкое описание названия **columnfamaly** и название столбцов
