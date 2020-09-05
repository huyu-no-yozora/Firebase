# GitLab CI - Trouble Shooting

## Firebase
### deploy
* firebase deploy時のScripting Error
  * 確認ポイント
    ```
    環境変数 FIREBASE_TOKEN をprotected branchのみ展開するように設定していた場合に、
    対象のbranchをprotectedに設定し忘れていないか。
    ```
