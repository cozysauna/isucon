# isucon


## 最初にやること

1. SQLにログがでるように設定【ISUCON本:148P】
pt-query-digest（←こっちのほうが詳細）【227P】
mysqldumpslow【151】
で遅いクエリを解析する

設定方法
my.cnfを書き換える

mysqldumpslowのインストール
```
brew install mysqldumpslow
mysqldumpslow <logファイル>
```


pt-query-digestのインストール
```
brew install percona-toolkit
pt-query-digest <logファイル>
```


2. nginxのログをjsonの形に整形【119P】
→alpコマンドで分析

設定方法
nginx.confを書き変える

alpコマンドのインストール
```
apt update
apt install wget
wget https://github.com/tkuchiki/alp/releases/download/v1.0.12/alp_linux_arm64.tar.gz
tar -zxvf alp_linux_arm64.tar.gz
install alp /usr/local/bin/alp
```

alp実行
```
cat access.log | alp json
```
レスポンスタイムの合計が多い順↓
```
alp json \
	--sort sum -r \
	-m "/posts/[0-9]+,@\w+,/image/\d+" \
	-o count,method,uri,min,avg,max,sum \
	< access.log
```

## 解析方法
1. SQLのログをpt-query-digest（mysqldumpslow）で解析

1. topコマンドを実行しながらベンチマーカーを実行

1. alpコマンドを使用し


## 改善案
- クエリのN+1問題
    - explainコマンド
    - indexを張る
        - force index
    - join（N*N→N）【498P】
    
- nginxの静的コンテンツキャッシュ配信
- unicorn workerプロセスの設定
- 外部コマンド呼び出しをやめる【519P】
    - ライブラリに置き換え