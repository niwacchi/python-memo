# Pythonと科学技術計算
## 科学技術計算
- データを対象
- 数式を用いた解析
- 数式を用いたシュミレーション

## 求められること
- マシンリソースの効率的な利用
- 高速な処理
- 可読性
- メンテナンス性

## Pythonの特徴
- それ自体での高速なプログラムは難しい場合がある。
- 他のプログラミング言語で記述されたコンポーネントと結合しやすい（グルー（糊）言語）
- 様々なデータソースとのデータ連携
- ビジュアライゼーション
- 科学技術計算に適した言語

## 主要な科学技術計算パッケージ
### SciPy Stack
- Pythonによる科学技術計算の中核をなすパッケージ群
#### NumPy
- 多次元配列を用いた効率的な数値計算のためのパッケージ
#### SciPy Library
- 高度な科学技術計算のためのパッケージ
#### Matplotlib
- グラフ描画のためのパッケージ
#### IPython
- 高度な機能を持つ対話型シェル
#### pandas
- 効率的なデータ処理のためのパッケージ
#### Sympy
- CAS(Computer Algebra System、計算機代数システム)のような記号計算を行うパッケージ
#### nose
- テストフレームワーク

### (パッケージ構成)
```sh
Python
 |- Numpy
     |- SciPy
     |- pandas
     |- Matplotlib
 |- IPython
 |- Sympy
 |- nose
```

### SciPy Stack以外の主なパッケージ
#### 機械学習
- scikit-learn
#### トピックモデル
- gensim
#### ディープラーニング
- Tensorflow, Chainer, PyTorch
#### 画像処理
- Pillow, OpenCV, scikit-image
#### 大量データ処理
- h5py, PyTables
#### JIT(Just In Time)コンパイルによる処理高速化
- Numba, NumExpr
#### データの可視化
- Matplotlib, seaborn, Bokeh

## 仮想環境の構築とパッケージのインストール
```sh
$ mkdir science
$ cd science/
$ python3 -m venv science
$ source science/bin/activate
$ pip install numpy scipy pandas scikit-learn
```
- IPython, NumPy, SciPy, pandas, scikit-learnをインスール

### NumPy

#### 概要

- SciPy、pandasなどの依存パッケージでもある。
- C/C++, FORTRANで実装されたndarrayという型を統一した多次元配列オブジェクトと、それに対す操作関数を提供する。
- Python標準のリスト、タプルに比べて高速な配列演算を実現
###### 処理実行時間の比較

```sh
In [1]: import numpy as np                                                      

# NumPyの配列処理
In [2]: %timeit np.arange(10000) + 1                                            
89.7 µs ± 14.6 µs per loop (mean ± std. dev. of 7 runs, 10000 loops each)

# Pythonのリスト処理
In [3]: %timeit [i+1 for i in range(10000)]                                     
6.54 ms ± 751 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
```

#### 基本操作
##### 配列と数値の演算
```sh
In [1]: import numpy as np

# リストから配列生成
In [6]: a = np.array([1, 2, 3, 4])
In [7]: b = 2

# 配列と数値の足し算
In [8]: a + b
Out[8]: array([3, 4, 5, 6])

# 配列の要素ごとの演算
In [9]: a ** 2
Out[9]: array([ 1,  4,  9, 16])
```
##### 配列の要素ごとの演算
```sh
# arangeメソッドで0から8までの連番の配列を生成
# reshapeメソッドで3行3列の2次元配列に変更
In [10]: a = np.arange(9).reshape(3, 3)       In [11]: b = np.arange(2, 7, 2)               

In [12]: a                                    Out[12]: 
array([[0, 1, 2],
       [3, 4, 5],
       [6, 7, 8]])

In [13]: b                                    Out[13]: array([2, 4, 6])

# 配列の要素ごとの足し算
In [14]: a + b                                Out[14]: 
array([[ 2,  5,  8],
       [ 5,  8, 11],
       [ 8, 11, 14]])
```
- サイズや形状の異なる配列どうしであっても演算を行える。（内部的にブロードキャスティングを行うことで実現する。）
