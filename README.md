## リリースチェック項目

### リリース準備

- [ ] kubectlの向き先が本番環境に向いているか確認 ( `kubetool info` )
- [ ] 現状の動いている image の version を確認 ( `kubetool pod --rc=abema-gateway` )
- [ ] RC の更新はあるか (ない場合はチェックしないで下さい)
    - [ ] (RC 更新がある場合のみ) RCを apply
    - [ ] (RC 更新がある場合のみ) RCを edit して項目が反映されていることを確認
- [ ] #release にてリリースアナウンス
- [ ] #release に変更内容を投稿
- [ ] 今稼働している tag の version を記録（切り戻し用）

### デプロイ

- [ ] Githubの対象リポジトリのタグを Push する
- [ ] CircleCI の Job は正常に完了したか確認
- [ ] RC の image の version が新しい tag に更新されているか確認 ( `kubectl get rc abema-gateway -o=yaml` )
- [ ] [admin, admin-gateway以外] podを1つだけ更新 ( `kubetool reload --1 abema-gateway` )
- [ ] [admin, admin-gateway以外] 更新したpodのログを確認 ( `kubectl logs <pod-name>` )
- [ ] [admin, admin-gateway以外] 全てのpodの version を新しいタグに合わせる ( `kubetool fix-version abema-gateway --interval=15` )
- [ ] Pod の状態は全て running になっているか、restart がかかっていないか確認 ( `kubetool pod --rc==abema-gateway` )
- [ ] 稼働中の pod のイメージを確認 ( `kubetool pod --rc==abema-gateway` )

### 最終確認

- [ ] Cloud logging もしくは `kubectl logs` にて、エラーログが出力されていないか確認
- [ ] リリースしたサービスは正常に動いているか確認
- [ ] `abema-ops` の 該当の RC の yml を更新して、PR を出す
- [ ]  お疲れ様でした
