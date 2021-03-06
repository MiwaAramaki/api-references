# Unlink Box with other objects

## Overview

Delete a list of OData resources associated with Box

### Required Privileges
|Link Object|Required Privileges|
|:-|:-|
|Role|box<br>auth|
|Relation|box<br>social|
|Rule|box<br>rule|

### Restrictions

* Accept in the request header is ignored
* Always handles Content-Type in the request header as application/json
* Only accepts the request body in the JSON format
* Only application/json is supported for Content-Type in the request header and the JSON format for the response body
* $formatQuery options ignored


## Request

### Request URL

#### link with Role

```
/{CellName}/__ctl/Box(Name='{BoxName}',Schema='{SchemaURL}')/$links/
_Role(Name='{RoleName}',_Box.Name='{BoxName}')
```

or 

```
/{CellName}/__ctl/Box(Name='{BoxName}')/$links/_Role(Name='{RoleName}',_Box.Name='{BoxName}')
```

or 

```
/{CellName}/__ctl/Box('{BoxName}')/$links/_Role(Name='{RoleName}',_Box.Name='{BoxName}')
```

#### link with Relation

```
/{CellName}/__ctl/Box(Name='{BoxName}',Schema='{SchemaURL}')/$links/_Relation(Name='{RelationName}',
_Box.Name='{BoxName}')
```

or 

```
/{CellName}/__ctl/Box(Name='{BoxName}')/$links/_Relation(Name='{RelationName}',_Box.Name='{BoxName}')
```

or 

```
/{CellName}/__ctl/Box('{BoxName}')/$links/_Relation(Name='{RelationName}',_Box.Name='{BoxName}')
```

#### link with Rule
```
/{CellName}/__ctl/Box(Name='{BoxName}',Schema='{SchemaURL}')/$links/
_Rule(Name='{RuleName}',_Box.Name='{BoxName}')
```

or 

```
/{CellName}/__ctl/Box(Name='{BoxName}')/$links/_Rule(Name='{RuleName}',_Box.Name='{BoxName}')
```
or 

```
/{CellName}/__ctl/Box('{BoxName}')/$links/_Rule(Name='{RuleName}',_Box.Name='{BoxName}')
```

If the Schema is omitted, it is assumed that null is specified

### Request Method

DELETE

### Request Query

|Query Name|Overview|Effective Value|Required|Notes|
|:--|:--|:--|:--|:--|
|p_cookie_peer|Cookie Authentication Value|The cookie authentication value returned from the server during authentication|No|Valid only if no Authorization header specified<br>Specify this when cookie authentication information is to be used|

### Request Header

|Header Name|Overview|Effective Value|Required|Notes|
|:--|:--|:--|:--|:--|
|X-HTTP-Method-Override|Method override function|User-defined|No|If you specify this value when requesting with the POST method, the specified value will be used as a method.|
|X-Override|Header override function|${OverwrittenHeaderName}:${Value}override} $: $ {value}|No|Overwrite normal HTTP header value. To overwrite multiple headers, specify multiple X-Override headers.|
|X-Personium-RequestKey|RequestKey field value output in the event log|Single-byte alphanumeric characters, hyphens ("-"), and underscores ("_")<br>Maximum of 128 characters|No|PCS-${UNIXtime} by default|
|Authorization|Specifies authentication information in the OAuth 2.0 format|Bearer {AccessToken}|No|* Authentication tokens are the tokens acquired using the Authentication Token Acquisition API|
|If-Match|Specifies the target ETag value|ETag value|No|[*] by default|

### Request Body

None


## Response

### Response Code

204

### Response Header

|Header Name|Overview|Notes|
|:--|:--|:--|
|DataServiceVersion|OData version||
|Access-Control-Allow-Origin|Cross domain communication permission header|Return value fixed to "*"|
|X-Personium-Version|API version that the request is processed|Version of the API used to process the request|

### Response Body

None

### Error Messages

Refer to [Error Message List](004_Error_Messages.md)


## cURL Command

```sh
curl "https://{UnitFQDN}/{CellName}/__ctl/Box('{BoxName}')/\$links/_Role(Name='{RoleName}',_Box.Name='{BoxName}')" \
-X DELETE -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json'
```


