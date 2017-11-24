# Relation List Acquire

### Overview

acquire existed Relation

### Restrictions

None

### OData Restrictions

* Accept in the request header is ignored
* Always handles Content-Type in the request header as application/json
* Only accepts the request body in the JSON format
* Only application/json is supported for Content-Type in the request header and the JSON format for the response body
* $formatQuery options ignored

### Required Privileges

social-read

<br>

### Request

#### Request URL

```
/{CellName}/__ctl/Relation
```

#### Request Method

GET

#### Request Query

The following query parameters are available

| Query Name<br>    | Overview<br>                    | Effective Value<br>                                                                | Required<br> | Notes<br>                                                                                                                |
|:-- |:-- |:-- |:-- |:-- |
| p_cookie_peer<br> | Cookie Authentication Value<br> | The cookie authentication value returned from the server during authentication<br> | No<br>       | Valid only if no Authorization header specified<br>Specify this when cookie authentication information is to be used<br> |

[\$select  Query](406_Select_Query.html)

[\$expand  Query](405_Expand_Query.html)

[\$format  Query](404_Format_Query.html)

[\$filter  Query](403_Filter_Query.html)

[\$inlinecount  Query](407_Inlinecount_Query.html)

[\$orderby  Query](400_Orderby_Query.html)

[\$top  Query](401_Top_Query.html)

[\$skip  Query](402_Skip_Query.html)

[Full-text Search (q) Query](408_Full_Text_Search_Query.html)

#### Request Header

| Header Name<br>            | Overview<br>                                       | Effective Value<br>                                                                                        | Required<br> | Notes<br>                                                                                                         |
|:-- |:-- |:-- |:-- |:-- |
| X-HTTP-Method-Override<br> | Method override function<br>                       | User-defined<br>                                                                                           | No<br>       | If you specify this value when requesting with the POST method, the specified value will be used as a method.<br> |
| X-Override<br>             | Header override function<br>                       | ${OverwrittenHeaderName}:${Value}<br>                                                                      | No<br>       | Overwrite normal HTTP header value. To overwrite multiple headers, specify multiple X-Override headers.<br>       |
| X-Personium-RequestKey<br> | RequestKey field value output in the event log<br> | Single-byte alphanumeric characters, hyphens ("-"), and underscores ("_")<br>Maximum of 128 characters<br> | No<br><br>   | PCS-${UNIXtime} by default<br>Supported in V 1.1.7 and later<br>                                                  |

#### OData Request Header

| Header Name<br>   | Overview<br>                                                     | Effective Value<br>      | Required<br> | Notes<br>                                                                                          |
|:-- |:-- |:-- |:-- |:-- |
| Authorization<br> | Specifies authentication information in the OAuth 2.0 format<br> | Bearer {AccessToken}<br> | No<br>       | * Authentication tokens are the tokens acquired using the Authentication Token Acquisition API<br> |

#### OData Create Request Header

| Header Name<br> | Overview<br>                           | Effective Value<br>  | Required<br> | Notes<br>                         |
|:-- |:-- |:-- |:-- |:-- |
| Accept<br>      | Specifies the response body format<br> | application/json<br> | No<br>       | [application/json] by default<br> |

#### Request Body

None

#### Request Sample

None

<br>

### Response

#### Response Code

200

#### Response Header

None

#### Response Body

The response is a JSON object, the correspondence between the key (name) and type defined in the object (subobject) and the value are as follows

| Object<br> | Item Name<br>   | Data Type<br> | Notes<br>                                       |
|:-- |:-- |:-- |:-- |
| Root<br>   | d<br>           | object<br>    | Object{1}<br>                                   |
| {1}<br>    | results<br>     | array<br>     | Array object {2}<br>                            |
| {2}<br>    | __metadata<br>  | object<br>    | Object{3}<br>                                   |
| {3}<br>    | uri<br>         | string<br>    | URL to the resource that was created<br>        |
| {3}<br>    | etag<br>        | string<br>    | Etag value<br>                                  |
| {2}<br>    | __published<br> | string<br>    | Creation date (UNIX time)<br>                   |
| {2}<br>    | __updated<br>   | string<br>    | Update date (UNIX time)<br>                     |
| {1}<br>    | __count<br>     | string<br>    | Get number of results in $inlinecount query<br> |

#### Relation specific response body

| Object<br> | Item Name<br>  | Data Type<br> | Notes<br>               |
|:-- |:-- |:-- |:-- |
| {3}<br>    | type<br>       | string<br>    | CellCtl.Relation <br>   |
| {2}<br>    | Name<br>       | string<br>    | Relation name<br>       |
| {2}<br>    | _Box.Name <br> | string<br>    | Relational Box Name<br> |

#### Response Sample

```JSON
{
  "d": {
    "results": [
      {
        "__metadata": {
          "uri":
          "https://{UnitFQDN}/{CellName}/__ctl/Relation(Name='{RelationName}',_Box.Name='{BoxName}')",
          "etag": "W/\"1-1486538244016\"",
          "type": "CellCtl.Relation"
        },
        "Name": "{RelationName}",
        "_Box.Name": "{BoxName}",
        "__published": "/Date(1486538244016)/",
        "__updated": "/Date(1486538244016)/",
        "_Box": {
          "__deferred": {
            "uri": "https://{UnitFQDN}/{CellName}/__ctl/Relation(Name='{RelationName}',_Box.Name='{BoxName}')/_Box"
          }
        },
        "_ExtCell": {
          "__deferred": {
            "uri": "https://{UnitFQDN}/{CellName}/__ctl/Relation(Name='{RelationName}',_Box.Name='{BoxName}')/_ExtCell"
          }
        },
        "_ExtRole": {
          "__deferred": {
            "uri": "https://{UnitFQDN}/{CellName}/__ctl/Relation(Name='{RelationName}',_Box.Name='{BoxName}')/_ExtRole"
          }
        },
        "_Role": {
          "__deferred": {
            "uri": "https://{UnitFQDN}/{CellName}/__ctl/Relation(Name='{RelationName}',_Box.Name='{BoxName}')/_Role"
          }
        }
      },
      {
        "__metadata": {
          "uri":           "https://{UnitFQDN}/{CellName}/__ctl/Relation(Name='{RelationName}',_Box.Name='{BoxName}')",
          "etag": "W/\"1-1486538757303\"",
          "type": "CellCtl.Relation"
        },
        "Name": "{RelationName}",
        "_Box.Name": "{BoxName}",
        "__published": "/Date(1486538757303)/",
        "__updated": "/Date(1486538757303)/",
        "_Box": {
          "__deferred": {
            "uri": "https://{UnitFQDN}/{CellName}/__ctl/Relation(Name='{RelationName}',_Box.Name='{BoxName}')/_Box"
          }
        },
        "_ExtCell": {
          "__deferred": {
            "uri": "https://{UnitFQDN}/{CellName}/__ctl/Relation(Name='{RelationName}',_Box.Name='{BoxName}')/_ExtCell"
          }
        },
        "_ExtRole": {
          "__deferred": {
            "uri": "https://{UnitFQDN}/{CellName}/__ctl/Relation(Name='{RelationName}',_Box.Name='{BoxName}')/_ExtRole"
          }
        },
        "_Role": {
          "__deferred": {
            "uri": "https://{UnitFQDN}/{CellName}/__ctl/Relation(Name='{RelationName}',_Box.Name='{BoxName}')/_Role"
          }
        }
      }
    ]
  }
}
```

#### Error Messages

Refer to [Error Message List](004_Error_Messages.html)

### cURL Command

```sh
curl "https://{UnitFQDN}/{CellName}/__ctl/Relation" -X GET -i  -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json'
```

<br><br><br><br><br>

###### Copyright 2017 FUJITSU LIMITED