# Boxと他オブジェクトとのリンク一覧取得
## 概要
Boxに紐付いたODataリソースを一覧取得する  
以下のODataリソースを指定することができる  

* Role
* Relation
* Rule

### 必要な権限
|紐付け先|必要な権限|
|:-|:-|
|Role|box-read<br>auth-read|
|Relation|box-read<br>social-read|
|Rule|box-read<br>rule-read|


### 制限事項
* リクエストヘッダのAcceptは無視される
* リクエストヘッダのContent-Typeは全てapplication/jsonとして扱う
* リクエストボディはJSON形式のみ受け付ける
* レスポンスヘッダのContent-Typeはapplication/jsonのみをサポートし、レスポンスボディはJSON形式とする


## リクエスト
### リクエストURL
#### Roleとの紐付け
```
/{CellName}/__ctl/Box(Name='{BoxName}',Schema='{SchemaURL}')/$links/_Role
```
または、
```
/{CellName}/__ctl/Box(Name='{BoxName}')/$links/_Role
```
または、
```
/{CellName}/__ctl/Box('{BoxName}')/$links/_Role
```
#### Relationとの紐付け
```
/{CellName}/__ctl/Box(Name='{BoxName}',Schema='{SchemaURL}')/$links/_Relation
```
または、
```
/{CellName}/__ctl/Box(Name='{BoxName}')/$links/_Relation
```
または、
```
/{CellName}/__ctl/Box('{BoxName}')/$links/_Relation
```
#### Ruleとの紐付け
```
/{CellName}/__ctl/Box(Name='{BoxName}',Schema='{SchemaURL}')/$links/_Rule
```
または、
```
/{CellName}/__ctl/Box(Name='{BoxName}')/$links/_Rule
```
または、
```
/{CellName}/__ctl/Box('{BoxName}')/$links/_Rule
```
※ Schemaパラメタを省略した場合は、nullが指定されたものとする

### メソッド
GET

### リクエストクエリ
以下のクエリパラメタが利用可能です。

|クエリ名|概要|有効値|必須|備考|
|:--|:--|:--|:--|:--|
|p_cookie_peer|クッキー認証値|認証時にサーバから返却されたクッキー認証値|×|Authorizationヘッダの指定が無い場合のみ有効<br>クッキーの認証情報を利用する場合に指定する|

<!---
[$select クエリ](406_Select_Query.md)

[$expand クエリ](405_Expand_Query.md)

[$format クエリ](404_Format_Query.md)

[$filter クエリ](403_Filter_Query.md)

[$inlinecount クエリ](407_Inlinecount_Query.md)

[$orderby クエリ](400_Orderby_Query.md)
-->

[$top クエリ](401_Top_Query.md)

[$skip クエリ](402_Skip_Query.md)

<!---
[全文検索(q)クエリ](408_Full_Text_Search_Query.md)
-->

### リクエストヘッダ

|ヘッダ名|概要|有効値|必須|備考|
|:--|:--|:--|:--|:--|
|X-HTTP-Method-Override|メソッドオーバーライド機能|任意|×|POSTメソッドでリクエスト時にこの値を指定すると、指定した値がメソッドとして使用されます。|
|X-Override|ヘッダオーバライド機能|${上書きするヘッダ名}:${値}|×|通常のHTTPヘッダの値を上書きします。複数のヘッダを上書きする場合はX-Overrideヘッダを複数指定します。|
|X-Personium-RequestKey|イベントログに出力するRequestKeyフィールドの値|半角英数、-(半角ハイフン)と_(半角アンダーバー)<br>最大128文字|×|指定がない場合、PCS-${UNIX時間}を設定する|
|Authorization|OAuth2.0形式で、認証情報を指定する|Bearer {AccessToken}|×|※認証トークンは認証トークン取得APIで取得したトークン|
|Accept|レスポンスボディの形式を指定する|application/json|×|省略時は[application/json]として扱う|
### リクエストボディ
なし


## レスポンス
### ステータスコード
200

### レスポンスヘッダ

|ヘッダ名|概要|備考|
|:--|:--|:--|
|Content-Type|返却されるデータの形式||
|DataServiceVersion|ODataのバージョン||
|Access-Control-Allow-Origin|クロスドメイン通信許可ヘッダ|返却値は"*"固定|
|X-Personium-Version|APIの実行バージョン|リクエストが処理されたAPIバージョン|
### レスポンスボディ

|オブジェクト|項目名|Data Type|備考|
|:--|:--|:--|:--|
|ルート|d|object|オブジェクト{1}|
|{1}|results|array|オブジェクト{2}の配列|
|{2}|uri|string|紐付いているODataリソースへのURL|
### エラーメッセージ一覧
[エラーメッセージ一覧](004_Error_Messages.md)を参照

### レスポンスサンプル
```JSON
{
  "d": {
    "results": [
      {
        "uri": "https://{UnitFQDN}/{CellName}/__ctl/Role(Name='{RoleName}',_Box.Name='{BoxName}')"
      }
    ]
  }
}
```

## cURLサンプル

```sh
curl "https://{UnitFQDN}/{CellName}/__ctl/Box('{BoxName}')/\$links/_Role" -X GET -i -H \
'Authorization: Bearer {AccessToken}' -H 'Accept: application/json'
```

