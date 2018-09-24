
macOSで環境構築
Homebrewをインストール
brew install python
python3
pip3

- パッケージ一覧の作成
-- 手動
``sh
echo 'パッケージ' >> requirements.txt
``
-- 全パッケージ情報
``sh
pip freeze > constraints.txt
``

- パッケージ一覧による一括インストール
``sh
pip3 install -r requirements.txt -c constarints.txt 
``

仮想環境の作成
有効化
無効化

対話モード
IPython

