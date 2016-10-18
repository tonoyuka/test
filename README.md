## リリースチェック項目

### リリース準備

- [ ] `kubetool info` kubectlの向き先が本番環境に向いているか
- [ ] 現状の動いている image の version を確認したか
- [ ] RC の更新はあるか (ない場合はチェックしないで下さい)
    - [ ] (RC 更新がある場合のみ) RCを apply したか
    - [ ] (RC 更新がある場合のみ) RCを edit して項目が反映されていることを確認したか
- [ ] #release にてリリースアナウンスをしたか
- [ ] #release に変更内容を投稿したか
- [ ] 今稼働している tag の version を記録したか（切り戻し用）

### デプロイ

- [ ] Githubの対象リポジトリのタグが Push されているか
- [ ] CircleCI の Job は正常に完了したか
- [ ] RC の image の version が新しい tag に更新されているか
- [ ] kubetool reload --1 を使って1個だけpodを更新したか (admin, admin-gatewayはなし)
- [ ] kubectl logs <pod-name> を使って更新したpodのログを確認したか (admin, admin-gatewayはなし)
- [ ] kubetool fix-version abema-gateway --interval=15 を使って全てのpodのバージョンを新しいタグに合わせたか (admin, admin-gatewayはなし)
- [ ] Pod の状態は全て running になっているか、restart がかかっていないか
- [ ] kubetool pods を実行し、稼働中の pod のイメージを確認したか

### 最終確認

- [ ] Cloud logging もしくは kubectl logs にて、エラーログが出力されていないか
- [ ] リリースしたサービスは正常に動いているか
- [ ] `abema-ops` の 該当の RC の yml を更新して、PR を出したか
- [ ]  お疲れ様でした
