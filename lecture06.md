## 第６回課題 
###  CloudTrailのイベントからAWSを利用した記録を確認
- イベント名
    - CreateTrail

- 含まれている内容を３つピックアップ
    - eventTime : 2023-10-10T12:47:35Z
    - awsRegion : ap-mortheast-1
    - eventCategory : Management

### ALBのアラームの設定
- CloudWatch Alarmで、アラームを作成。
- ターゲットグループのヘルスチェックの結果が１分間に１回以上Unhealthyとなった場合にアラーム状態となりメール通知されるよう設定。
- また、アラーム状態からOK状態になったときも、メール通知されるように設定した。
![CloudWatch Alarm](/Image/lecture06/lecture06_1.png)  
![CloudWatch Alarm](/Image/lecture06/lecture06_2.png)
- サンプルアプリのWEBサーバーを停止し、アラーム状態となったことを通知するメールが届くことを確認した。  
![Alarm](/Image/lecture06/lecture06_3.png)  
![Alarm mail](/Image/lecture06/lecture06_4.png)
- サンプルアプリのWEBサーバーを起動し、OK状態に戻ったことを通知するメールが届くことを確認した。  
![OK](/Image/lecture06/lecture06_5.png)  
![OK mail](/Image/lecture06/lecture06_6.png)

### AWS利用料の見積
- 今日までに作成したリソースの内容を見積もった。  
[AWS利用料の見積書](https://calculator.aws/#/estimate?id=ab93dd726bb597fd7175d4272dc68e605b7d14a6)

### 先月の請求情報の確認
- 先月の利用料は、無料枠の範囲内に収まっていた。  
![先月の請求](/Image/lecture06/lecture06_7.png)

### 今回の課題から学んだこと
試しにConfigを設定してみたら、今月の請求見積額が有料になったほか、もうすぐS3の無料上限枠に達するという旨の通知が来た。  
サービスを使用するに当たっては、事前にどの程度料金がかかるか調べた上で使用する必要があると感じた。 