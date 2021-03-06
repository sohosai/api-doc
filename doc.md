# 筑波大学学園祭 雙峰祭 2014 年度 企画情報 API ドキュメント

このドキュメントに関する詳細は `/README.md` をご覧ください。

API の利用に際し認証や開発者登録等は必要ありませんが、大量のアクセスを実施する予定が有る場合などは事前に学園祭実行委員会 (info[at]sohosai.com) までお問い合わせください。

## API エンドポイント

### ベース URI

`https://login.sohosai.tsukuba.ac.jp`

注意: 現在上記ホストでは CVE-2014-3566 への対応として、暫定的に SSL 3.0 のサポートを取りやめています。

### `GET /search/api/projects`

#### リクエスト

| パラメータ  | 必須 | 型     | 説明                                                                 |
|-------------|------|--------|----------------------------------------------------------------------|
| keyword     | yes  | string | 検索キーワード。企画名、企画説明、企画運営団体名のいずれかにマッチ。 |
| area_id     | no   | int    | 企画実施エリア。詳細は下記対応表を参照。                             |
| category_id | no   | int    | 企画種別。詳細は下記対応表を参照。                                   |
| does_cook   | no   | bool   | 調理企画の場合は true                                                |
| day_eve     | no   | bool   | 前夜祭参加企画の場合は true                                          |
| day_one     | no   | bool   | 1日目参加企画の場合は true                                           |
| day_two     | no   | bool   | 2日目参加企画の場合は true                                           |

#### レスポンス

以下に説明するパラメータを含む連想配列の配列。検索条件に該当する企画が存在しない場合は空の配列が返される。

| パラメータ    | 説明                                          |
|---------------|-----------------------------------------------|
| account_id    | 企画 ID。企画グランプリの投票などに使用       |
| account_name  | 企画運営者名                                  |
| name          | 企画名                                        |
| description   | 企画説明。パンフレット用原稿のもの            |
| area_id       | 企画実施エリアの ID。詳細は下記対応表を参照   |
| area          | 企画実施エリア                                |
| detail_area   | 企画実施場所。屋内の場合は教室名などを含む    |
| is_indoor     | 屋内実施企画の場合は true                     |
| category_id   | 企画種別 ID。詳細は下記対応表を参照           |
| category_name | 企画種別                                      |
| does_cook     | 調理企画の場合は true                         |
| day_eve       | 前夜祭参加企画の場合は true                   |
| day_one       | 1日目参加企画の場合は true                    |
| day_two       | 2日目参加企画の場合は true                    |

#### 例

##### `GET /search/api/projects?keyword=ITF`

企画名、企画説明、企画運営団体のいずれかに ITF を含むすべての企画情報を配列として返す。

##### `GET /search/api/projects?keyword=ITF&does_cook=false&day_one=true`

下記の条件をすべて満たす企画の情報を配列として返す。

- 企画名、企画説明、企画運営団体のいずれかに ITF を含む
- 調理企画でない
- 一日目に参加 (実施) する

## 参考

### 企画実施エリア ID 対応表

| ID         | エリア                   |
|------------|--------------------------|
| (空文字列) | 指定なし                 |
| X          | エリア未確定             |
| 1          | 第一エリア (屋外)        |
| 2          | 第一エリア (屋内)        |
| 3          | 第二・第三エリア (屋外)  |
| 4          | 第二・第三 (屋内)        |
| 5          | 会館エリア (屋外)        |
| 6          | 会館エリア (屋内)        |
| 7          | 体芸エリア (屋外)        |
| 8          | 体芸エリア (屋内)        |
| 9          | ステージ                 |
| 0          | 移動企画                 |


### 企画種別 ID 対応表

| ID             | 企画種別        |
|----------------|-----------------|
| normal         | 一般            |
| stage_normal   | 一般ステージ    |
| academic       | 学研            |
| stage_academic | 学研ステージ    |
| miniature      | ミニチュア学研  |




