- yamlファイルをkubectlで実行する方法
```shell
kubectl apply -f 〇〇.yml
```
- yamlファイルを削除する
```shell
kubectl delete -f 〇〇.yml 
```

- 全体を確認する
```shell
kubectl get all 
```

- replicasetを確認する
```shell
kubectl get rs
```

- podの中で定義したcontainerに入ることができる
```shell
kubectl exec -it Pod名 sh
```

## Replicasetとは
- 常に指定したレプリカ数のpodを保つようになっている
- Deploymentからreplicasetを管理する。
- フィールド
  - replicas：稼働させたいPodの数
  - pod templates：Podを作成するときのテンプレート
  - selector：対象となるPodを特定するため
## Deploymentとは
  - ローリングアップデートやロールバックなどのアップデート機能を提供
  - 主な機能
    - Replicasetのロールアウト(更新)
    - 不安定な場合の前のバージョンへロールバック(戻す)
    - スケールアップ、ダウン。(replica数変更)
  - 特有のフィールド
    - strategy：更新処理
      - type：RecreateかRollingUpdateを指定
        - デフォルトはRollingUpdate
      - RollingUpdateの場合には
        - maxUnavaliable:更新処理中に利用不可になるPodの最大数
        - maxSurge；更新処理にいくつかのエクストラで追加できるPodの最大数
      - revisionHistory：過去のバージョンとしてReplicaSetを残しておく
      - paused：一時停止されているかどうか
      - progressDeadlineSeconds：更新プログレスの最大秒数
        - デフォルトは600sec