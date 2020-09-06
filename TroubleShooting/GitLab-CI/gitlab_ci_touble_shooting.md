# GitLab CI - Trouble Shooting

## GitLab - Specific Runner
### CI job 
  #### CI setting error
  以下のようなErrorが発生した時
  ```
  This job is stuck because the project doesn't have any runners online assigned to it. Go to project CI settings.
  ```
  * 解決策
  1. .gitlab-ci.ymlで、jobにtagを付与。
     ```yaml
     [your-job]:
       tags:
         - hoge
     ```
  1. gitlab-runner registerで、1.で付与したtagを付与（カンマ区切りで入力）


## Firebase
### deploy
* firebase deploy時のScripting Error
  * 確認ポイント
    ```
    環境変数 FIREBASE_TOKEN をprotected branchのみ展開するように設定していた場合に、
    対象のbranchをprotectedに設定し忘れていないか。
    ```
