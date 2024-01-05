## 第10回課題 
CloudFormationを利用して、第５回までに作った環境をコード化

#### 第５回までに作った環境
![構成図](/Image/lecture05/lecture05_9.png)

#### テンプレート
以下の５つのテンプレートを作成した。
- [Network](/lecture10/Network.yml) : VPC、サブネット、IGW、ルートテーブル
- [Instances](/lecture10/Instances.yml) : EC2、RDS、セキュリティグループ
- [alb](/lecture10/alb.yml) : ALB、ターゲットグループ、セキュリティグループ
- [storage](/lecture10/storage.yml) : S3バケット、VPCエンドポイント
- [iam](/lecture10/iam.yml) : IAMロール


#### 作成したリソースの確認
###### リソースマップ
![リソースマップ](/Image/lecture10/lecture10_01_map.png)
###### サブネット
![サブネット](/Image/lecture10/lecture10_02_subnet.png)
###### パブリックサブネットのルートテーブル
![ルートテーブル](/Image/lecture10/lecture10_03_RoutetableForPublicSubnet.png)
###### EC2インスタンス
![EC2](/Image/lecture10/lecture10_04_EC2.png)
![EC2](/Image/lecture10/lecture10_05_EC2.png)
###### RDSインスタンス
![RDS](/Image/lecture10/lecture10_06_RDS.png)
![RDS](/Image/lecture10/lecture10_07_RDS.png)
###### ロードバランサー
![ALB](/Image/lecture10/lecture10_08_ALB.png)
###### ターゲットグループのターゲット
![ターゲット](/Image/lecture10/lecture10_09_ALBTarget.png)
###### ロードバランサーのインバウンドルール
![ALBインバウンドルール](/Image/lecture10/lecture10_10_ALB.png)
###### S3バケット
![S3](/Image/lecture10/lecture10_11_S3.png)
###### VPCエンドポイント
![VPCエンドポイント](/Image/lecture10/lecture10_12_VPCEndpoint.png)
###### IAMロール
![IAMロール](/Image/lecture10/lecture10_13_IAMrole.png)