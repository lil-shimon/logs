[TOC]

# Docker





## Error

### no space left on devise

it causes due to lack of devise memory. in case using docker, there are no room for strage.

#### check percentage of using

```
df -h
```



#### === reference ===

find /ファイル数の多いディレクトリ名 -xdev -type f | cut -d "/" -f 3 | sort | uniq -c | sort -nr



#### 効果があった解決方法

```
docker volume rm `docker volume ls -q -f dangling=true`
```

https://qiita.com/sakymark/items/df58ea2fd9179eddc566

