# 背景/Requirements  
あるアプリケーションはAWS様々なサービスを利用して構築されている、当該プロジェクトはnon-criticalであり、起動時間も非定期的である。
AWS Lambda関数(Infrastructure As Code)でアプリケーションの基盤施設のLaunch・クリアを一環管理している。且つ、当該Lambda関数がWebServiceとしてインタネットで公開されている。  
コスト削減のため、  
①基盤施設起動：  
アプリケーション利用したい場合SNOWでマネージャーの承認フローを行って、アプリケーションをLaunchする。  
②基盤施設削除：  
毎日退勤時間に基盤施設をチェックし、存在する場合削除を行う。　  
上記②についてAWS Lambdaでバッチ機能として実装されました。AWSとSNOWの機能連携で①の要件を実装するのが本プロジェクトの要点である  
# 設計  
SnowのServer-Side Scriptで公開されたAWS Lambda関数(Infrastructure As Code)を呼び出す
# そのた  
