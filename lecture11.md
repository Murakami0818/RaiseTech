## 第11回課題 
Serverspecのテストを実行

### 事前準備
第10回の課題で自動構築したEC2で、第５回の課題と同様に、git等のパッケージ、ruby、Budler、Rails、Node、yarn、Nginx等をインストールし、NginxとUnicornでサンプルアプリケーションを起動できる状態にした。

### Serverspecのインストールとセットアップ
##### Serverspecのインストール
```
$ gem install serverspec
```

##### Serverspecのセットアップ
```
$ serverspec-init
Select OS type:

  1) UN*X
  2) Windows

Select number: 1

Select a backend type:

  1) SSH
  2) Exec (local)

Select number: 2　　　# Serverspecをインストールしたサーバー内でテストを行うため、localを選択。

Vagrant instance y/n: n

 + spec/
 + spec/localhost/
 + spec/localhost/sample_spec.rb
 + spec/spec_helper.rb
 + Rakefile
 + .rspec
```

### テストの実行
##### テストコードの作成
```ruby
require 'spec_helper'

listen_port = 80

# Nginxのインストール確認
describe package('nginx') do
  it { should be_installed }
end

# ポートの確認
describe port(listen_port) do
  it { should be_listening }
end

# ステータスコードの確認
describe command('curl http://127.0.0.1:#{listen_port}/_plugin/head/ -o /dev/null -w "%{http_code}\n" -s') do
  its(:stdout) { should match /^200$/ }
end

# パッケージのインストール確認
%w{make gcc-c++ patch libyaml-devel libffi-devel libicu-devel zlib-devel readline-devel libxml2-devel libxslt-devel ImageMagick ImageMagick-devel openssl-devel libcurl libcurl-devel curl git}.each do |pkg|
  describe package(pkg) do
    it { should be_installed }
  end
end

# Rubyのバージョン確認
describe command('ruby -v') do
  its(:stdout) { should match /ruby 3\.1\.2/ }
end

# Bundlerのバージョン確認
describe command('bundler -v') do
  its(:stdout) { should match /Bundler version 2\.3\.14/ }
end

#　Railsのバージョン確認
describe command('rails -v') do
  its(:stdout) { should match /Rails 7\.0\.4/ }
end

# Nodeのバージョン確認
describe command('node -v') do
  its(:stdout) { should match /v17\.9\.1/ }
end

# Nginxの起動確認
describe service('nginx') do
  it { should be_running }
end
```

##### 実行結果
![実行結果](/Image/lecture11/lecture11_01.png) 
![実行結果](/Image/lecture11/lecture11_02.png) 
![実行結果](/Image/lecture11/lecture11_03.png) 

### 学んだこと・感想
- Serverspecを使用するに当たり参考にしたサイトでは、SSH接続を選択しているものが多かった。直接サーバーにインストールしなくても、SSH接続することによりテストできることがServerspecの利用しやすい点であることが分かった。
- 正規表現について学んだ（バージョンを表す`.`の前に`\`が必要な理由等）。

