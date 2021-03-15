[TOC]

# Docker





## Error

## no space left on devise

it causes due to lack of devise memory. in case using docker, there are no room for strage.

### check percentage of using

```
df -h
```



#### === reference ===

find /ファイル数の多いディレクトリ名 -xdev -type f | cut -d "/" -f 3 | sort | uniq -c | sort -nr

### ９割解決コマンド

```
docker volume rm `docker volume ls -q -f dangling=true`
```



```
# activeでないvolumesを確認する
docker system df
# dangling volumeのリストを確認
docker volume ls -q -f dangling=true
# 参照されてないvolumesを削除
docker volume rm `docker volume ls -q -f dangling=true`
```



#### delete all images

```
docker images -aq | xargs docker rmi
```



#### delete all container

```
docker ps -aq | xargs docker rm
```



#### delete a image that have chlid dependency

```
docker rmi -f test:0.91
```