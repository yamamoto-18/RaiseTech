# RaiseTech
2023年12月1日より、オンラインスクール「[RaiseTech](https://raise-tech.net/courses-lp/aws-full-course)」にてAWSコースの受講を開始しました。<br>
第16回まである授業の内、第10回までの受講・課題提出が済んでおり、第11回は現在学習中、それ以降は今後学習予定となっております。<br>
当GitHub上で、これまでに取り組んだ課題の内容が確認できます。

<br>
<br>

| 授業 № | 主な学習内容 | 課題 |
|:---:|---|---|
| 1 | - 授業の概要<br> - AWSとは | - AWSアカウント作成<br> - IAMの推奨設定<br> - Cloud9の作成<br> - Rubyを実行して「Hello World」を表示 |
| 2 | - バージョン管理システム<br> - Git<br> - GitHub<br> - Markdown | **[lecture02](./lecture02.md)**<br> - GitHubアカウントを作成<br> - Git設定<br> - Pull Request |
| 3 | - Webアプリケーションとは<br> - システム開発の流れ<br> - 外部ライブラリと構成管理の重要性 | **[lecture03](./lecture03.md)**<br> - Railsサンプルアプリケーションのデプロイ<br> - APサーバー、DBサーバーについて |
| 4 | - AWSでの権限管理<br> - EC2・RDSとは | **[lecture04](./lecture04.md)**<br> - IAM権限管理とAWS上でのネットワーク ～ EC2、RDSの作成 |
| 5 | - ELB・S3について<br> - インフラ構成図 | **[lecture05](./lecture05.md)**<br> - EC2上でアプリケーションのデプロイ<br> - ELBとS3の構築<br> - 構成図の作成 |
| 6 | - システムの安定稼働とAWSでの実装・確認 | **[lecture06](./lecture06.md)**<br> - CloudTrailのイベント確認<br> - CloudWatchアラームの動作確認<br> - AWS利用料の見積書を作成<br> - コスト管理|
| 7 | - システムにおけるセキュリティの基礎<br> - セキュリティ対策 | **[lecture07](./lecture07.md)**<br> - 考察と対策|
| 8 | - 第4回・第5回授業課題の実演 | ― |
| 9 | - 第4回・第5回授業課題の実演 | ― |
| 10 | - CloudFormation | **[lecture10](./lecture10.md)**<br> - AWS環境のコード化 |
| 11 | - インフラのコード化を支援するツール<br> - インフラのテストとは<br> - テスト駆動環境<br> - ServerSpec | **学習中 / 課題未提出**<br>- ServerSpec のテスト（予備課題） |
| 12 | - Terraformの解説<br> - DevOps<br> - CI/CDツールとは | **今後学習予定 / 課題未実施**<br>- CircleCI のサンプルコンフィグの組み込み（予備課題） |
| 13 | - 構成管理ツールとは<br> - Ansible<br> - OpsWorks<br> - CircleCIとの併用 | **今後学習予定 / 課題未実施**<br>- CircleCI のサンプルに ServerSpec や Ansible の処理を追加（予備課題） |
| 14 | - 第13回授業課題の実演 | **今後視聴予定 / 課題未実施**<br> - AWS 構成図、自動化処理がわかる図、リポジトリのREADME作成 |
| 15 | - 第13回授業課題の実演 | **今後視聴予定 / 課題なし** |
| 16 | - 現場へ出ていくにあたって | **今後視聴予定 / 課題なし** |

<br>
<br>
<br>

## CloudFormationで構築した環境

<br>
<br>

![Alt text](images-README/aws-readme.png)

<br>
<br>
<br>

第10回目の授業課題では、これまでの課題で構築した環境（上図）をCloudFormationでコード化し、自動で環境が構築されることを確認するところまで行いました。作業手順は以下の通りです。<br>
**※ 作成したテンプレートは[こちら](./lecture10.md)で確認ができます**

<br>

1. CloudFormationについて下調べをする
2. テンプレートファイルの構成を考える
3. テンプレートファイルに記述する項目を精査する
4. スタックを作成し、エラーが出れば解消を試みる
5. 構築された環境が第4回・第5回授業課題で作成した環境と同一のものかを確認する

<br>

### 【 工夫した点 】
- 既存の環境とリファレンスページを見比べ、テンプレートに記述するリソースを厳選した
- MyIPやPasswordをハードコードしないようにした
- エラーの解消速度向上のために、VSCodeにcfn-lintを導入した
- 課題に取り組みながら[lecture10](./lecture10.md)に過程をまとめ、どこで躓いたか等の振り返りができるようにした

<br>
<br>

## 2024年5月現在
- AWS Certified Solutions Architect - Associate 取得済み
- RaiseTech AWSコース 第11回授業課題に取り組む
- ITパスポート試験を受験するため学習を継続中