# 多次元配列

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

# 二次元配列の要素取り出し

```python
print(b[1,2]) # = b[1][2] 三次元以上も同様にインデックス増やしていくことで取り出せる
```

# axis

引数にaxisを指定した場合、特定の方向での計算可能

```python
print(np.sum(b, axis=0)) #vertical
print(np.sum(b, axis=1)) #horizontal
```



