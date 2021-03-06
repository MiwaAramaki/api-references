# ComplexTypeProperty削除
## 概要
既存のComplexTypeProperty情報を削除する
### 必要な権限
alter-schema
### 制限事項
* リクエストヘッダのContent-Typeは全てapplication/jsonとして扱う
* リクエストボディはJSON形式のみ受け付ける
* レスポンスヘッダのContent-Typeはapplication/jsonのみをサポートし、レスポンスボディはJSON形式とする
* $formatクエリオプションにatom または xmlを指定した場合、エラーとはならないが、レスポンスボディのデータの保証はない
	- 削除対象に関係性設定が存在する場合、削除は実行されません。
	- ComplexTypePropertyを削除する場合は、削除対象のComplexTypePropertyを使用しているEntityTypeのユーザデータが存在しない場合のみ削除可能
```
例)
EntityTypeA
   │ PropertyA Type-String
   └ PropertyB Type-ComplexTypeA
                 └ ComplexTypePropertyA
ComplexTypePropertyAを削除する場合は、 EntityTypeAのデータが存在しない場合のみ可能
```


## リクエスト
### リクエストURL
```
/{CellName}/{BoxName}/{ODataCollecitonName}/$metadata/ComplexTypeProperty(Name='
{ComplexTypePropertyName}',_ComplexType.Name='{ComplexTypeName}')
```
### メソッド
DELETE
### リクエストクエリ
#### 共通リクエストクエリ
|クエリ名|概要|有効値|必須|備考|
|:--|:--|:--|:--|:--|
|p_cookie_peer|クッキー認証値|認証時にサーバから返却されたクッキー認証値|×|Authorizationヘッダの指定が無い場合のみ有効<br>クッキーの認証情報を利用する場合に指定する|
#### OData 共通リクエストクエリ
なし
### リクエストヘッダ
#### 共通リクエストヘッダ
|ヘッダ名|概要|有効値|必須|備考|
|:--|:--|:--|:--|:--|
|X-HTTP-Method-Override|メソッドオーバーライド機能|任意|×|POSTメソッドでリクエスト時にこの値を指定すると、指定した値がメソッドとして使用される|
|X-Override|ヘッダオーバライド機能|${上書きするヘッダ名}:${値}|×|通常のHTTPヘッダの値を上書きします。複数のヘッダを上書きする場合はX-Overrideヘッダを複数指定する|
|X-Personium-RequestKey|イベントログに出力するRequestKeyフィールドの値|半角英数、-(半角ハイフン)と_(半角アンダーバー)<br>最大128文字|×|指定がない場合、PCS-${UNIX時間}を設定する|
#### OData共通リクエストヘッダ
|ヘッダ名|概要|有効値|必須|備考|
|:--|:--|:--|:--|:--|
|Authorization|OAuth2.0形式で、認証情報を指定する|Bearer {AccessToken}|×|※認証トークンは認証トークン取得APIで取得したトークン|
#### OData削除クエストヘッダ
|ヘッダ名|概要|有効値|必須|備考|
|:--|:--|:--|:--|:--|
|If-Match|対象ETag値を指定する|ETag値|×|省略時は[*]として扱う|
### リクエストボディ
なし


## レスポンス
### ステータスコード
204
### レスポンスヘッダ
なし
### レスポンスボディ
なし
### エラーメッセージ一覧
[エラーメッセージ一覧](004_Error_Messages.md)を参照


## cURLサンプル

```sh
curl "https://{UnitFQDN}/{CellName}/{BoxName}/{ODataCollecitonName}/\$metadata/ComplexTypeProperty\
(Name='{ComplexTypePropertyName}',_ComplexType.Name='{ComplexTypeName}')" -X DELETE -i -H \
'Authorization: Bearer {AccessToken}' -H 'Accept: application/json'
```

