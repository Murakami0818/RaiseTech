## 第５回課題 
### 組み込みサーバーだけでサンプルアプリケーションをデプロイ
- パッケージ一式のインストール後、Ruby、Node、yarn、bundlerをインストールし、config/database.ymlにRDSのエンドポイントを記載して起動。
- ブラウザで「（パブリックIPアドレス）:3000」にアクセスし、起動できていることを確認。
![組み込みサーバー](/Image/lecture05/lecture05_1.png)

### WEBサーバーとAPサーバーを分けてサンプルアプリケーションをデプロイ
- Nginxをインストールし、EC2のセキュリティグループでHTTP接続が可能となるよう設定を変更。
- ブラウザからパブリックIPアドレスにアクセス。正常にインストールされ、動作していることを確認。
![Nginx](/Image/lecture05/lecture05_2.png)
- Nginx設定ファイルを作成し、Unicornのソケットファイルのパスやpublicディレクトリのパス等を記載。
- さらに、Nginxユーザーがこれらのパスにアクセスできるよう、権限の設定を変更。
- Unicornを起動してブラウザからHTTP接続し、正常に起動できていることを確認。
![Nginx+Unicorn](/Image/lecture05/lecture05_3.png)

### ALBの追加
- ALBを作成し、EC2のセキュリティグループのインバウンドルールで、HTTP通信をALBのセキュリティグループのみに変更。
- ブラウザでALBのDNSにアクセスし、接続を確認。
![ALB追加](/Image/lecture05/lecture05_4.png)

### S3の追加
- S3にフルアクセスできるように権限を有したIAMロールを作成し、EC2にアタッチ。
![IAMロール](/Image/lecture05/lecture05_5.png)
- VPCエンドポイントを作成。ポリシーは、S3の特定のバケットに対してのみ操作可能となるよう設定。
![VPCエンドポイント](/Image/lecture05/lecture05_6.png)
- AWS CLIでEC2からS3に接続し、EC2からS3のバケットにファイルをアップロードしたり削除したりできることを確認。
- config/environments/development.rbファイルで、「config.active_storage.service = 」を「:local」から「:amazon」に変更。
- config/storage.ymlファイルで、S3の箇所のバケット名を、作成したバケット名に変更。
- サンプルアプリで画像をアップロードし、S3に保存されることを確認した。
![S3へアップロード](/Image/lecture05/lecture05_7.png)
![S3に保存](/Image/lecture05/lecture05_8.png)

### 構成図
![構成図](/Image/lecture05/lecture05_9.png)

### 今回の課題から学んだこと
- viコマンドでファイルを編集する方法
- development＝開発環境、test＝テスト環境、production＝本番環境という３種類の環境があること
- GemfileとGemfile.lockの関係
- ユーザーにはrootユーザーと一般ユーザーとシステムユーザーの３通りがあること
- 上位のディレクトリと下位のディレクトリで権限の設定が異なる場合、上位のディレクトリの権限が優先して適用されること（たとえば下位のディレクトリが701であっても、上位のディレクトリが700であれば、Otherは下位のディレクトリの実行権限を持たない。）
- IAMロールの概念と、IAMポリシーのJSON形式での表記の仕方