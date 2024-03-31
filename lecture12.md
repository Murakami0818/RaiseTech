## 第12回課題
[CircleCI のサンプルコンフィグ](https://github.com/MasatoshiMizumoto/raisetech_documents/tree/main/aws/samples/circleci)をリポジトリに組み込み、動作させる。

### 事前準備
GitHubの課題提出用のリポジトリに新たに[lecture12ディレクトリ](/lecture12)を作成し、第10回の課題で作成したCloudFormationのテンプレートファイルのうち[alb.ymlファイル](/lecture10/alb.yml)をコピーして格納。

### CircleCIとGitHubの連携
GitHubのアカウントでCircleCIにサインインし、RaiseTechの課題提出用のGitHubリポジトリを選択してプロジェクトを作成。

### .circleci/config.ymlファイルの作成
- CircleCI公式ドキュメントの[スタートガイド](https://circleci.com/docs/ja/getting-started/)を参考に、まずはサンプルとして提供されているHelloWorldを表示させる.circleci/config.ymlファイルを作成。
![HelloWorld](/Image/lecture12/lecture12_1.png)
- 次に、作成した.circleci/config.ymlの内容を、課題で提供されたサンプルコンフィグの内容に書き換えた。  
[.circleci/config.yml](.circleci/config.yml)
![サンプルconfig](/Image/lecture12/lecture12_2.png)

### 自動テストの実行
第10回の課題で作成したCloudFormationのテンプレートファイルのうち、以下の４つのファイルをコピーして[lecture12ディレクトリ](/lecture12)に加え、`git push`を実行。
- [instances.yml](/lecture10/instances.yml)
- [network.yml](/lecture10/network.yml)
- [iam.yml](/lecture10/iam.yml)
- [storage.yml](/lecture10/storage.yml)

### 実行結果
以下のとおりエラーが表示された。
![実行結果](/Image/lecture12/lecture12_3.png)

### テンプレートファイルの修正
- [Instances.ymlファイル](/lecture12/Instances.yml)で、パスワードを指定するパラメータに、`NoEcho: true`の記載を追加。
- [Instances.ymlファイル](/lecture12/Instances.yml)と[Network.ymlファイル](/lecture12/Network.yml)でアベイラビリティゾーンをハードコーディングしてしまっていたので、パラメータを設定。

### テンプレートファイルの修正後の実行結果
エラーが解消され、テストが成功した。
![実行結果](/Image/lecture12/lecture12_4.png)

### 学んだこと
#### CircleCI関係
- ワークフローでコマンドが実行されるディレクトリは、`working_directory`で指定しない限りデフォルトでは「/home/circleci/project」になる。
- `checkout`により、working_directoryで指定したディレクトリ（指定しない場合は上記のデフォルトのディレクトリ）にリポジトリの内容が展開される。
#### CloudFormation関係
- パラメータを設定する際、`NoEcho`属性を`true`に設定すると、マネジメントコンソール等で値がマスクされる。パスワード等の重要情報をパラメータとして渡す場合は、`NoEcho: true`を設定することで安全性を高められる。
#### その他
- コマンドやディレクトリ名を打ち込むときは、Tabキーの補完機能を使うと入力ミスを減らすことができる。
