# Acquire ExtRole

## Overview

acquire existed ExtRole

### Required Privileges

social

### Restrictions

* OData Restrictions
    * Accept in the request header is ignored
    * Always handles Content-Type in the request header as application/json
    * Only accepts the request body in the JSON format
    * Only application/json is supported for Content-Type in the request header and the JSON format for the response body
    * $formatQuery options ignored

### Required Privileges

auth-read

## Request

### Request URL

```
/{CellName}/__ctl/ExtRole
```

### Request Method

GET

### Request Query

|Query Name|Overview|Effective Value|Required|Notes|
|:--|:--|:--|:--|:--|
|p_cookie_peer|Cookie Authentication Value|The cookie authentication value returned from the server during authentication|No|Valid only if no Authorization header specified<br>Specify this when cookie authentication information is to be used|

[$select  Query](406_Select_Query.md)

[$expand  Query](405_Expand_Query.md)

[$format  Query](404_Format_Query.md)

### Request Header

|Header Name|Overview|Effective Value|Required|Notes|
|:--|:--|:--|:--|:--|
|X-HTTP-Method-Override|Method override function|User-defined|No|If you specify this value when requesting with the POST method, the specified value will be used as a method.|
|X-Override|Header override function|${OverwrittenHeaderName}:${Value}|No|Overwrite normal HTTP header value. To overwrite multiple headers, specify multiple X-Override headers.|
|X-Personium-RequestKey|RequestKey field value output in the event log|Single-byte alphanumeric characters, hyphens ("-"), and underscores ("_")<br>Maximum of 128 characters|No|PCS-${UNIXtime} by default|
|Authorization|Specifies authentication information in the OAuth 2.0 format|Bearer {AccessToken}|No|* Authentication tokens are the tokens acquired using the Authentication Token Acquisition API|
|Accept|Specifies the response body format|application/json|No|[application/json] by default|


## Response

### Response Code

200

### Response Body

#### Common

The response is a JSON object, the correspondence between the key (name) and type defined in the object (subobject) and the value are as follows

|Object|Item Name|Data Type|Notes|
|:--|:--|:--|:--|
|Root|d|object|Object{1}|
|{1}|results|array|Array object {2}|
|{2}|__published|string|Creation date (UNIX time)|
|{2}|__updated|string|Update date (UNIX time)|
|{2}|__metadata|object|Object{3}|
|{3}|uri|string|URL to the resource that was created|
|{3}|etag|string|Etag value|
|{1}|__count|string|Get number of results in $inlinecount query|

### ExtRole specific response body

|Object|Item Name|Data Type|Notes|
|:--|:--|:--|:--|
|{3}|type|string|CellCtl.ExtRole|
|{2}|ExtRole|string|External Role URL|
|{2}|_Relation.Name|string|Relation Name|
|{2}|_Relation._Box.Name|string|Box Name aassociated wirh Relation|

### Error Messages

Refer to [Error Message List](004_Error_Messages.md)

### Response Sample

```JSON
{
  "d": {
    "results": {
      "__metadata": {
        "uri": "https://{UnitFQDN}/{CellName}/__ctl/ExtRole(ExtRole='https://{UnitFQDN}/{CellName}
/__role/__/{ExtRoleName}',_Relation.Name='{RelationName}',_Relation._Box.Name='{BoxName}')",
        "etag": "W/\"1-1486717404966\"",
        "type": "CellCtl.ExtRole"
      },
      "ExtRole": "https://{UnitFQDN}/{CellName}/__role/__/{ExtRoleName}",
      "_Relation.Name": "{RelationName}",
      "_Relation._Box.Name": "{BoxName}",
      "__published": "/Date(1486717404966)/",
      "__updated": "/Date(1486717404966)/",
      "_Role": {
        "__deferred": {
          "uri": "https://{UnitFQDN}/{CellName}/__ctl/ExtRole(ExtRole='https://{UnitFQDN}/{CellName}
/__role/__/{ExtRoleName}',_Relation.Name='{RelationName}',_Relation._Box.Name='{BoxName}')/_Role"
        }
      },
      "_Relation": {
        "__deferred": {
          "uri": "https://{UnitFQDN}/{CellName}/__ctl/ExtRole(ExtRole='https://{UnitFQDN}/{CellName}
/__role/__/{ExtRoleName}',_Relation.Name='{RelationName}',_Relation._Box.Name='{BoxName}')/_Relation"
        }
      }
    }
  }
}
```


## cURL Command

```sh
curl "https://{UnitFQDN}/{CellName}/__ctl/ExtRole(ExtRole='https%3A%2F%2F{UnitFQDN}%2F{CellName}\
%2F__role%2F__%2F{ExtRoleName}',_Relation.Name='{RelationName}',_Relation._Box.Name='{BoxName}')" \
-X GET -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json'
```

