# vPremisesの実装と紹介範囲

2026-10-15に公開sourceを確認。vPremisesは環境の構成・変更計画・結果の記録・検査とコンテナ基盤を扱うOSS組織である。ローカルObserverは製品CLIの一機能で、組織全体の説明とは分ける。

| 正本 | 実装されている機能 | 実運用と分ける範囲 |
|---|---|---|
| environment-deployment/crates/environment-deployment/src | schema/profile解決、digest、SQLite Ledger、replay拒否、保守window/timer描画 | provider接続、plan適用、timer有効化は行わない |
| environment-deployment/crates/incus-renderer/src/render.rs | 制限付きIncus project/profile/instanceのOpenTofu JSON | 実リソース作成・証明書受入は別 |
| environment-operations/apps/environment-plan/src/main.rs | resolve/plan/make-receipt/record/render-maintenance CLI | 合成receiptは実適用の証明ではない |
| environment-operations/apps/security-inspector/src/cli | doctor/observe/audit/report/OSS検査、限定された内容・ネットワークの収集器連携 | root/検出器/namespace/上限を明示、全端末認証ではない |
| environment-operations/native/windows-custody-helper | Windows custody helper実行ファイル | 署名・WSL接続・実資格情報登録は独立受入 |
| port-office/images/debian/Dockerfile | Debian最小OS、非root、CA trust、UTF-8、UTC | Python/Node/製品を同梱せず、GHCR公開前の候補 |
| cloud-router/*/compose*.yaml | Docker Swarm/TraefikのHTTP/HTTPS例、制限したDocker APIとdigest検証 | 実stack起動・TLS発行・運用は別 |
| azure-openemr | OpenEMRホスト配備とNGINX保護ディレクトリの回帰検証 | Azure自動構築、医療サービス本番運用の保証はしない |

認可された実行・資格情報保管・共通観測はCrowsi、汎用データ/API連携はZixcel、環境向けの製品構成とCLIはvPremisesに置く。実profile/登録/運用データの非公開正本は紹介データに含めない。

公開repoの存在/archived状態をGitHubで再確認した。azure-openemrは公開GPL-3.0のため、その表示を保持し、他repoのApache-2.0へ一律に変更しない。実行・公開済みと確認していない機能を利用可能なサービスとして案内しない。
