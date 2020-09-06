# GitLab Runner

## 注意点
* Mac OSの場合、`/srv`の部分は`/Users/Shared`とする。

## Runnerのインストール/設定
```yaml:docker-compose.yml
version: '3'
services:
  runner:
    image: gitlab/gitlab-runner
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /srv/gitlab-runner/config:/etc/gitlab-runner
```

```bash
docker-compose up -d
```

```bash
docker-compose exec runner bash
gitlab-runner register
```
対話式で情報を登録していく。以下は設定例。
```yaml
url: https://gitlab.com/
token: [specific runner token]
image: ubuntu:latest
tag: docker,[その他タグ]
executer: docker
```

[非推奨] 以下のような形でも、設定できる。（tokenを履歴に入れないよう、こちらは非推奨とする）
```bash
docker-compose exec runner gitlab-runner register -n \
   --url "https://gitlab.com/" \
   --registration-token "[token]" \
   --executor "docker" \
   --description "GitLab Runner - Docker Runner" \
   --docker-image "docker:stable" \
   --tag-list docker \
   # --docker-volumes "/var/run/docker.sock:/var/run/docker.sock"
```

### .gitlab-ci.ymlファイルの編集
Jobにtagをつける。以下は例。
```
job:
  tags:
      - docker
```
> [参考]
> jobにtagをつけて動作させないと、
> ```
> This job is stuck because the project doesn't have any runners online assigned to it. Go to project CI settings.
> ```
> という警告で、保留となる。
> 
> ※tagをつけないで、実行したい場合は、GitLab側のRunnerの設定（の編集）画面にて、  
> Run untagged jobsの項目（`Indicates whether this runnner can pick jobs without tags`）にチェックを入れる。


## その他
```bash
docker run -d --name gitlab-runner --restart always \
           -v /var/run/docker.sock:/var/run/docker.sock \
           -v /srv/gitlab-runner/config:/etc/gitlab-runner \
           gitlab/gitlab-runner:latest

docker run --rm -t -i -v /srv/gitlab-runner/config:/etc/gitlab-runner gitlab/gitlab-runner register
```


## Reference
* GitLab: https://docs.gitlab.com/runner/install/docker.html#docker-image-installation


