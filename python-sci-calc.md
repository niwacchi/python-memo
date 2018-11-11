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

#### ファイル入出力
```sh
In [1]: a = np.arange(9).reshape(3,3)                           
In [2]: b = np.arange(2, 7, 2)

# 変数aの内容をテキストファイルに出力
In [3]: np.savetxt('data.txt',a)                                                
# lsコマンドで確認
In [4]: !ls data.txt                                            data.txt

# テキストファイルの読み込み
# dtypeはデータ型指定
In [5]: np.loadtxt('data.txt', dtype=np.uint8)                 Out[5]: 
array([[0, 1, 2],
       [3, 4, 5],
       [6, 7, 8]], dtype=uint8)

# 変数aの内容をバイナリファイルに出力
# 拡張子npyが自動的に付加
In [6]: np.save('data',a)

# バイナリファイルの読み込み
In [7]: np.load('data.npy')               
Out[7]: 
array([[0, 1, 2],
       [3, 4, 5],
       [6, 7, 8]])

# 変数aと変数bの内容をxとyの名前で１つのバイナリファイルに出力
# 拡張子npzが自動的に付加
In [8]: np.savez('data2', x=a, y=b)

# 複数の配列データを読み込み
In [9]: c = np.load('data2.npz')                                In [10]: c['x']
Out[10]: 
array([[0, 1, 2],
       [3, 4, 5],
       [6, 7, 8]])
In [11]: c['y']                                                 Out[20]: array([2, 4, 6])
```

#### 関数操作
##### NumPyの機能群と関数例 ※詳細はNumPyのAPIリファレンス参照
| 機能                   | 関数                                |
| ---------------------- | ----------------------------------- |
| 配列操作               | np.array, np.arange                 |
| インデックス操作       | np.where, np.select                 |
| 数学関数               | np.sin, np.cos, np.mod              |
| 線形代数演算           | np.dot, np.linalg.det, np.linalg.gr |
| 統計関数               | np.mean, np.std, np.histogram       |
| 多項式展開             | np.polynomial.polynomial            |
| ランダムサンプリング   | np.rand, np.randint,np.choice       |
| ソート、検索、カウント | np.sort, np.argmax                  |
| 窓関数                 | np.hamming                          |
| バイナリ演算           | np.bitwise                          |
| 高速フーリエ変換       | np.fft,np.ifft                      |

```sh
# 表示有効桁数を２桁に設定
# 表示列を先頭末尾をそれぞれ２列に設定
# 指数を非表示に設定
In [25]: np.set_printoptions( 
    ...:     precision=2,edgeitems=2,suppress=True)

# 乱数を固定するためのseedを設定
In [26]: np.random.seed(0)                                      

# 0から100の間のランダムな変数９個をもつ配列を生成
In [27]: a = np.random.randint(0,100,9)                         In [28]: a                                                      Out[28]: array([44, 47, 64, 67, 67,  9, 83, 21, 36])

# 配列aの要素の最大値を出力
In [29]: a.max()
Out[29]: 83

# 配列aの要素の中からランダムに３つの要素を選択
In [30]: np.random.choice(a,3)                                  
Out[30]: array([21, 83, 36])

# 配列aを3行3列の2次元配列に整形
In [31]: b = a.reshape(3,3)
In [32]: b
Out[32]: 
array([[44, 47, 64],
       [67, 67,  9],
       [83, 21, 36]])

# bの逆配列を計算
In [33]: np.linalg.inv(b)                                       Out[33]: 
array([[-0.01,  0.  ,  0.02],
       [ 0.01,  0.02, -0.02],
       [ 0.02, -0.01,  0.  ]]) 
```

### SciPy
#### 概要
- NumPyの機能をベースとしている。
- 科学技術計算アルゴリズムを提供（Netlibというライブラリ群に含まれるCもしくはFORTRAN実装にPythonインタフェース提供したもの）
#### サブパッケージ
- 詳細はSciPyの公式ドキュメントを参照
- 線形代数演算、高速フーリエ変換はNumPyにも存在するが、一般的にはSciPyのほうが高機能かつ高速

|サブパッケージ|説明|
|--|--|
|scipy.special|特殊関数|
|scipy.integrate|常微分方程式と積分のソルバー|
|scipy.optimize|最適化と適合|
|scipy.interpolate|補間|
|scipy.fftpack|高速フーリエ変換|
|scipy.signal|信号処理|
|scipy.linalg|線形代数演算|
|scipy.stats|統計と乱数|
|scipy.ndimage|画像処理|
|scipy.io|ファイル入出力|

#### 例
##### QR分解
```sh
In [34]: from scipy import random, linalg, allclose             

# ランダムな値を取る3行2行配列を作成
In [35]: a = random.randn(3,2)                                  In [36]: a                                                      Out[36]: 
array([[-0.1 ,  0.41],
       [ 0.14,  1.45],
       [ 0.76,  0.12]])

# QR分解を実行
In [37]: q, r = linalg.qr(a)

# QとRの内容を確認
In [38]: q
Out[38]: 
array([[-0.13, -0.31,  0.94],
       [ 0.18, -0.94, -0.28],
       [ 0.97,  0.14,  0.18]])
In [39]: r
Out[39]: 
array([[ 0.78,  0.33],
       [ 0.  , -1.48],
       [ 0.  ,  0.  ]])

# QとRのサイズ確認
In [40]: q.shape, r.shape
Out[40]: ((3, 3), (3, 2))

# A=QRが成立することを確認
In [41]: allclose(a, np.dot(q,r))
Out[41]: True
```

### pandas
#### 概要
- データ処理を行うパッケージ。データ解析ツール
- NumPyをベースとした数表や時系列データを操作するためのデータ構造と操作関数を提供
- 様々なデータソースやフレームワークとの連携において中心的な役割を果たす。

#### データ構造と機能概要
- Seriesと呼ばれる１次元配列とDatframeと呼ばれる2２次元配列の２つのデータ構造を持つ。
##### 可能な操作
- インデックスを用いたデータ操作
- 様々なデータフォーマット間の入出力
- 欠損値の処理
- データ構造の変更やピボット
- 大きなデータの分割、サブセット化
- データの連結、グループごとの集約
- 時系列データに対する日付範囲の生成、ウインドウごとの統計処理
#### pandas DataFrameによるデータ処理
##### UCI Machine Learning Repository
- http://archive.ics.uci.edu/ml/
##### データセットのダウンロード
- http://archive.ics.uci.edu/ml/datasets/Abalone
##### pandasの操作
```sh
In [43]: import pandas as pd

# 表示桁数を２桁に設定
In [45]: pd.set_option('precision', 2)                                          

# abaloneのデータの読み込み
# namesは列名、usecolsは読み込む列番号の設定
In [46]: df = pd.read_csv('abalone.data', names=('性別', '殻長', '殻幅', '高さ',
    ...:  '重さ', '年輪'), usecols=[0,1,2,3,4,8])                               

# データのスキーマ情報の表示
In [47]: df.dtypes                                                              
Out[47]: 
性別     object
殻長    float64
殻幅    float64
高さ    float64
重さ    float64
年輪      int64
dtype: object

# 年齢(年輪+1.5)列を追加
In [48]: df['年齢'] = df['年輪'] + 1.5
In [49]: df.head()                                                              
Out[49]: 
  性別    殻長    殻幅    高さ    重さ  年輪    年齢
0  M  0.46  0.36  0.10  0.51  15  16.5
1  M  0.35  0.27  0.09  0.23   7   8.5
2  F  0.53  0.42  0.14  0.68   9  10.5
3  M  0.44  0.36  0.12  0.52  10  11.5
4  I  0.33  0.26  0.08  0.20   7   8.5

# locメソッドで列名を指定して抽出
In [50]: df2 = df.loc[:, ['殻長', '殻幅', '高さ']]                              

# 統計情報を表示
In [51]: df2.describe()                                                         
Out[51]: 
            殻長       殻幅       高さ
count  4177.00  4177.00  4177.00
mean      0.52     0.41     0.14
std       0.12     0.10     0.04
min       0.07     0.06     0.00
25%       0.45     0.35     0.12
50%       0.55     0.42     0.14
75%       0.61     0.48     0.17
max       0.81     0.65     1.13
```

### scikit-learn
#### 概要
- 機械学習アルゴリズムを集めたパッケージ
- Numpy、SciPyがベース
#### 公式サイト
- https://scikit-learn.org/stable/

#### 主な機能
- 分類(離散データに対するカテゴリの推定)
- 回帰(連続データに対する推定)
- クラスタリング(類似データのグルーピング)
- 次元削減(データを表現する特徴量数の削減)
- モデル選択(パラメータチューニングや交差検証)
- データ前処理(特徴量の抽出、変換、選択)

#### 機械学習モデルの開発例
- 推定する変数＝目的変数
- 目的変数を説明する変数＝説明変数
- 訓練データを使用してモデルを学習し、未知のデータに対して推定を行う方法＝教師あり学習
##### 機械学習の前処理
```sh
# データ前処理
# 性別データは、M（オス）、F（メス）、I（不明）からなる離散データ
# 性別データを0と1で表現する数値型の離散データに変換する。
# 0と1のフラグで表現する３つの列を持つ性別情報のDataFrameを生成
In [58]: df_sex = pd.get_dummies(df['性別'], prefix='性別')                     
In [59]: df_sex.head()                                                          
Out[59]: 
   性別_F  性別_I  性別_M
0     0     0     1
1     0     0     1
2     1     0     0
3     0     0     1
4     0     1     0

# df_sexとdfをjoinし、不必要な列を削除
# axis=1は行ではなく列の削除であることを示す
In [60]: train_data = df_sex.join(df).drop(['性別', '年輪'], axis=1)            
In [61]: train_data.head()                                                      
Out[61]: 
   性別_F  性別_I  性別_M    殻長    殻幅    高さ    重さ    年齢
0     0     0     1  0.46  0.36  0.10  0.51  16.5
1     0     0     1  0.35  0.27  0.09  0.23   8.5
2     1     0     0  0.53  0.42  0.14  0.68  10.5
3     0     0     1  0.44  0.36  0.12  0.52  11.5
4     0     1     0  0.33  0.26  0.08  0.20   8.5

# 訓練データは説明変数(アワビの特徴)と目的変数(年齢)を分けておく
# X_trainはすべての行の0から6列目
# y_trainはすべての行の7列目
In [62]: X_train = train_data.iloc[:, :7]                
In [63]: y_train = train_data.iloc[:, 7]                                        
In [64]: X_train.head()                                                         
Out[64]: 
   性別_F  性別_I  性別_M    殻長    殻幅    高さ    重さ
0     0     0     1  0.46  0.36  0.10  0.51
1     0     0     1  0.35  0.27  0.09  0.23
2     1     0     0  0.53  0.42  0.14  0.68
3     0     0     1  0.44  0.36  0.12  0.52
4     0     1     0  0.33  0.26  0.08  0.20

In [65]: y_train.head()                                                         
Out[65]: 
0    16.5
1     8.5
2    10.5
3    11.5
4     8.5
Name: 年齢, dtype: float64
```

##### 回帰モデルの学習と推定
- アワビの年齢という連続値を取る目的変数を推定＝回帰分析
- ランダムフォレストを利用する。
- scikit-learnのRandomForestRegressor
```sh
In [68]: from sklearn.ensemble import RandomForestRegressor                     

# 回帰モデルの定義
In [69]: model = RandomForestRegressor()                                        

# 訓練データを使って回帰モデルを構築
In [70]: model.fit(X_train, y_train)                                            
Out[70]: 
RandomForestRegressor(bootstrap=True, criterion='mse', max_depth=None,
           max_features='auto', max_leaf_nodes=None,
           min_impurity_decrease=0.0, min_impurity_split=None,
           min_samples_leaf=1, min_samples_split=2,
           min_weight_fraction_leaf=0.0, n_estimators=10, n_jobs=None,
           oob_score=False, random_state=None, verbose=0, warm_start=False)

# 訓練データに対する推定
In [71]: prediction = model.predict(X_train)   
```

##### 学習済みモデルの評価
- 通常の機械学習のプロセスでは、モデルの性能を評価し、パラメータチューニングを行う
- 実際のアワビの年齢と推定値がどの程度異なっているかをMSE（平均二乗誤差）と呼ばれる指標で確認
```sh
In [78]: from sklearn.metrics import mean_squared_error                         

# MSE(平均二乗誤差)の計算 
In [80]: mean_squared_error(y_train, prediction)                                
Out[80]: 1.3087090601973772
```

##### モデルとデータの永続化
- scikit-learnはpickleを利用したモデル永続化の仕組みを提供
```sh
In [81]: from sklearn.externals import joblib                                   

# モデルの保存
In [82]: joblib.dump(model, 'abalone_randomforest.pkl')                         
Out[82]: ['abalone_randomforest.pkl']

# データの保存
In [83]: y_train_prediction = np.array([y_train, prediction])                   
In [84]: np.save('y_train_prediction', y_train_prediction) 
```
