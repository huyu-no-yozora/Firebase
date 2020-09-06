# Firebase

## 利用について
```
Google Accountさえあれば、Credit Card無しでも利用可能（銀行口座登録なども必要ない）。
```


### Run a Docker Container on local environment
```
docker pull snoworld/swd-firebase
docker run --name [container name] -it -p 9005:9005 [image id] /bin/bash 
```


### Login
```
firebase login
```


### Initialize of your Project

#### 構成情報
```yaml
Project Name: silver-project

```

#### 手順
```
mkdir silver-project
cd silver-project
firebase init
firebase deploy
```


### CI
```
firebase login:ci
```
please note your CI Token.



## Trouble Shooting

### deploy
* firebase deploy
  * 確認ポイント
    ```
    環境変数`FIREBASE_TOKEN`をprotected branchのみ展開するように設定していた場合に、
    対象のbranchをprotectedに設定し忘れていないか。
    ```
    
