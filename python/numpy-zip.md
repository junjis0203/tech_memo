# NumPyでzip的なことをする

二つの二次元配列→タプルの二次元配列にしたい（`a[i, j]`と`b[i, j]`をペアにしたい）。`dstack`を使えばよい。

```py
In [1]: import numpy as np

In [2]: a = np.random.randint(10, size=(2, 5))

In [3]: b = np.random.randint(10, size=(2, 5))

In [4]: a
Out[4]:
array([[7, 8, 5, 9, 9],
       [6, 3, 7, 0, 2]])

In [5]: b
Out[5]:
array([[6, 5, 1, 7, 2],
       [3, 4, 7, 0, 1]])

In [6]: c = np.dstack((a, b))

In [7]: c
Out[7]:
array([[[7, 6],
        [8, 5],
        [5, 1],
        [9, 7],
        [9, 2]],

       [[6, 3],
        [3, 4],
        [7, 7],
        [0, 0],
        [2, 1]]])
```

逆にタプルの二次元配列（実際には三次元配列）から元の二次元配列を取り出すにはスライスすればよい。

```py
In [8]: c[:, :, 0]
Out[8]:
array([[7, 8, 5, 9, 9],
       [6, 3, 7, 0, 2]])

In [9]: c[:, :, 1]
Out[9]:
array([[6, 5, 1, 7, 2],
       [3, 4, 7, 0, 1]])
```

一次元配列をzip的にまとめたい場合は`dstack`ではなく`column_stack`を使う。`stack`の`axis`指定が一番汎用的だが二次元以上をまとめることはあまりないだろう。  
https://stackoverflow.com/questions/44409084/how-to-zip-two-1d-numpy-array-to-2d-numpy-array
