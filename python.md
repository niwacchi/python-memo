# Pythonメモ

## 環境構築
### macOS
- Homebrew

  https://brew.sh/index_ja

- Python
```sh
brew install python
```

- 動作確認
```sh
python3
```
# パッケージ管理ツール
## 使い方
```sh
pip3 install xxx
```
## パッケージ一覧
- 手動で作成
```sh
echo 'パッケージ' >> requirements.txt
```

- 全パッケージ情報を含んだ一覧の作成
```sh
pip freeze > constraints.txt
```

- パッケージ一覧による一括インストール
```sh
pip3 install -r requirements.txt -c constarints.txt 
```

## 仮想環境
```sh
# 作成
mkdir basis
python3 -m venv basis

# 有効化
source basis/bin/activate

# 無効化
deactivate
```

## 対話モード
- 「python」とタイプしてEnter


### IPython
- RPEL
- インストール
```sh
pip install ipython
```
- 起動
```sh
ipython
```

## Jupyter Notebook
- インストール
```sh
pip install jupyter
```
- 起動
```sh
jupyter notebook
```

