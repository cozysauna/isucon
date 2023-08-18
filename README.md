# isucon


## 最初にやること

1. SQLにログがでるように設定【ISUCON本:148P】
pt-query-digest（←こっちのほうが良い）
mysqldumpslow
で遅いクエリを解析する

設定方法
my.cnfのように設定する

2. nginxのログをjsonの形に整形
alpコマンドで分析

## 解析方法
1. SQLのログをpt-query-digest（mysqldumpslow）で解析

1. topコマンドを実行しながらベンチマーカーを実行


## 改善案
- クエリのN+1問題
    - explainコマンド
    - indexを張る
        - force index
    
- nginxの静的コンテンツキャッシュ配信
- unicorn workerプロセスの設定
- 外部コマンド呼び出しをやめる【519P】
    - ライブラリに置き換え