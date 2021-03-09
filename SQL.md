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



# With query expansion

これは、検索を 2 回実行することで機能します。2 回目の検索での検索フレーズは、1 回目の検索でのもっとも関連性の高い数個のドキュメントと連結されたオリジナルの検索フレーズです。したがって、これらのドキュメントのいずれかに単語 「databases」 および単語 「MySQL」 が含まれている場合は、単語 「database」 が含まれていなくても、2 回目の検索で単語 「MySQL」 を含むドキュメントが検索されます。

-->あいまい検索

```sql
mysql> SELECT * FROM articles
    WHERE MATCH (title,body)
    AGAINST ('database' WITH QUERY EXPANSION);
```

