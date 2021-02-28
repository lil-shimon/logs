## シンボリックリンク

　「ln -s」で、ファイルの“シンボリックリンク”を作成できます。シンボリックリンクは、いわばファイルの“別名”で、長いファイル名に別の名前を付けたり、パス名の指定が分かりにくい場所にあるファイルを扱いやすくしたりする（例：ディレクトリへのシンボリックリンク）場合に使います。

```
ln -s ファイル名 リンク名

（ファイルのシンボリックリンクを作成する）
```

## メモリ

| total  | メインメモリのサイズ |
| ------ | -------------------- |
| used   | メモリ使用量         |
| free   | メモリの空き容量     |
| shared | 共有メモリ           |
| buffer | バッファのキャッシュ |
| cached | ページのキャッシュ   |

https://www.sejuku.net/blog/54699

```
free -t 
free -m /// mega bite
free -g /// giga bite
top 
```

## 高速化

**Linuxのパフォーマンスを改善する3つのTips (1/3)**

https://www.itmedia.co.jp/enterprise/articles/0707/19/news012.html



## copy directory

```
cp -R ===== =====
```



## Check locale and keyboard

```
localectl
```

