# 1. 背景/Requirements  
あるアプリケーションはAWS様々なサービスを利用して構築されている、当該プロジェクトはnon-criticalであり、起動時間も非定期的である。
AWS Lambda関数(Infrastructure As Code)でアプリケーションの基盤施設のLaunch・クリアを一環管理している。且つ、当該Lambda関数がWebServiceとしてインタネットで公開されている。  
コスト削減のため、  
①基盤施設起動：  
アプリケーション利用したい場合SNOWでマネージャーの承認フローを行って、アプリケーションをLaunchする。  
②基盤施設削除：  
毎日退勤時間に基盤施設をチェックし、存在する場合削除を行う。　  
上記②についてAWS Lambdaでバッチ機能として実装されました。AWSとSNOWの機能連携で①の要件を実装するのが本プロジェクトの要点である  
# 2. 設計  
## 2.1 Data Modeling/データモデリング 
|カラム|タイプ|ラベル|
| :---        |    :----   |          :---- |
|request_id|String|申請ID|
|requester|String|申請者|
|service|Choice|サービス|
|action|Choice|アクション|
|ask_for_approver|Ref|指定承認者|
|dead_line|Date|承認期待期日|
|status|Choice|リクエストステータス|
|approved_by|String|承認実施者|
|approved_rejected_date|Date|承認・拒否日付|
|comment_his|Journal|コメント|

Choice型設定  
#### サービス  
- データベース
- FrontEnd
- BackEnd
- All
#### アクション
- 起動
- 停止
#### ステータス
- Ask for Approval
- Approved-JobOnRunning
- Approved-JobSucceed
- Approved-JobFailed
- Cancel
- Rejected

## 2.2 ステータス遷移図  
![cloudIacServicenow](https://github.com/sean-akatsuki/101.example_snow_awsiac/assets/18321490/78fa7ec5-3c9e-48cb-8d6d-fa26ecc1f113)

## 2.3 UI  
#### Appメニュー  
![cloudIac_app](https://github.com/sean-akatsuki/101.example_snow_awsiac/assets/18321490/5210c63d-9652-4560-bcbc-b736c279cb59)

#### Form  
![cloudIac_form](https://github.com/sean-akatsuki/101.example_snow_awsiac/assets/18321490/46080593-59d2-4fd9-8af5-283374a07fde)


