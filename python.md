# Numpy

## 多次元配列

```
import numpy as np
b = np.array([[1,2][3,4]]) #二次元配列

c = np.array([[[0,1,2],[3,4,5]],[[5,4,3][2,1,0]]]) #３次元配列をNumpyで作成
```

[[[0 1 2]

​	[3 4 5]]

 [[ 5 4 3]

   [2 1 0]]]

次元の異なる配列でもブロードキャストにより演算を行うことも可能。

縦の要素数、横の要素数を知りたい場合はshape method

変更したいことでreshape

```
print(a.shape) 			#(2,3)など
c = b.replace(2,4)  #(2,4)の二次元配列に変換
```

reshapeの引数を-1にするとどんな配列でも１次元配列に変換可能。

## 二次元配列の要素取り出し

```python
print(b[1,2]) # = b[1][2] 三次元以上も同様にインデックス増やしていくことで取り出せる
```

## axis

引数にaxisを指定した場合、特定の方向での計算可能

```python
print(np.sum(b, axis=0)) #vertical
print(np.sum(b, axis=1)) #horizontal
```

## linspace

```
x = np.lispace(-5, 5) #-5から5までの間を50の区間で区切る
```

## 自然対数log

```
def get_log(x):
	return np.log(x) # y = log X
	
print(get_log(1)) # 0.0 
```

## ネイピア数 

```
def get_exp:
	return np.exp(x)

print(get_exp(1)) 
```

## ∑

```
a = np.array([1, 2, 3, 4, 5])
print(np.sum(a))
```



## 分散

```
x = array (.....)
print (np.var(x))
```



# Matplotlib

グラフを描画するのにmatplotlib.pyplotをいうモジュールがある

データにはNumpyの配列を使う。

### Graph

```python
x = np.lispace(-5, 5) #x axis
y_1 = 2 * x #y axis
y_2 = 3 * x

#label
plt.xlabel("x value")
plt.ylabel("y value")

#title of graph
plt.title("My Graph")

# prot, style of line, explanatory notes
plt.plot(x, y_1, label="y1")
plt.plot(x, y_2, label="y2", linestyle="dashed")
plt.legend() #display explanatory notes

plt.show()
```

画像の表示や散布図の表示もできる。



# pickle

## Mode="wb"

ファイルを保存

## mode="rb"

ファイルをバイナリーモードで復元読み込み