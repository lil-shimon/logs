# Gopath不要

以下のコマンドでgo.modファイルを作成してくれる。

gopathの設定しなくても良い？

```
go mod init module name
```

# GOLAND

## 設定

https://qiita.com/keitakn/items/26946ee021a43a933799

# 公式チュートリアル

https://go-tour-jp.appspot.com/welcome/1



# 文法

最初に実行されるのはmainパッケージの中のmain func

```go
package main

func main () {
  
}
```

パッケージはプログラムを構成する単位のこと

メッセージを表示する命令はfmt(フォーマット)パッケージを使う

Printlnは値を改行付きで表示する関数

他のパッケージで読み込んだ命令の最初の一文字は必ず大文字

```go
fmt.Println("hello world")
```

## 変数

変数宣言、変数に値を代入

var Name Type = value　

stringが入ることが明示的な場合は方を省略可

```go
var name string = "hello world"
var name = "hello world"
```

宣言と代入はよく使うのでこのような書き方もできる

```
name := "hello world"
```

文字列と一緒に変数を使用するにはPrintlnではなく、Printfを使う

そのうえで変数を埋め込みたい位置に%vをいれて,変数名でOK

```go
name := "world"
fmt.Printf("hello %v", name)
fmt.Printf("hello %v again", name)
```

#### 入力を受け取る方法

コンピュータのメモリ上で guess の変数がある場所を指定するには、 &guess と書いてあげれば OK

```go
var guess int
fmt.Scanf("%v", &guess)
```

#### 条件分岐

```go
if A == B {
	
} else {
  
}
```

#### 乱数生成

math/rand

```go
//static

import (
  "math/rand"
)

a := rand.Intn(10) // 1~9

// dynamically
// add 
import ("time")
rand.Seed(time.Now().UnixNano())
```

#### 繰り返し

```go
for {
	// do something
  break
}
```

#### 増加

```go
// same
count = count + 1
count += 1
count++
```

