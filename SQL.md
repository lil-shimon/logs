## Delete Data Table(Drop Table)

```sql
DROP TABLE [IF EXISTS] tbl_name [, tbl_name] ...
```

In case you want to delete address table, it would be like this below

```sql
drop table address;
```

 

## Show Table

```sql
show tables;
```

## Create Data

```sql
INSERT INTO `product_types` (`id`, `name`) VALUES ('1', 'モニター');
INSERT INTO `product_types` (`id`, `name`) VALUES ('2', '計測機');
INSERT INTO `product_types` (`id`, `name`) VALUES ('3', 'JS');
INSERT INTO `product_types` (`id`, `name`) VALUES ('4', 'その他');
```

Update data (ALL)

```sql
UPDATE table_name SET column_name = 'the data you want to input'
```

# type

int(10)