# Get EntityType \$links list

### Overview

List OData resources associated with EntityType<br>
You can specify the following OData resources

* AssociationEnd

### Required Privileges

Unpublished

### Restrictions

* Always handles Content-Type in the request header as application/json
* Only accepts the request body in the JSON format
* Only application/json is supported for Content-Type in the request header and the JSON format for the response body
* Response body data is not ensured if atom or xml is specified in the $format query option, although it does not result in an error

<br>

### Request

#### Request URL

\$links with AssociationEnd

```
/{CellName}/{BoxName}/{CollectionName}/EntityType('{EntityTypeName}')/$links/_AssociationEnd
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

##### Common Request Header

| Header Name<br>            | Overview<br>                                       | Effective Value<br>                                                                                        | Required<br> | Notes<br>                                                                                                                    |
|:-- |:-- |:-- |:-- |:-- |
| X-HTTP-Method-Override<br> | Method override function<br>                       | User-defined<br>                                                                                           | No<br>       | Specifying this value in a request with the POST method indicates that the specified value is used as the method<br>         |
| X-Override<br>             | Header override function<br>                       | ${OverwrittenHeaderName}:${Value}<br>                                                                      | No<br>       | The normal HTTP header value is overwritten. Specify multiple X-Override headers for the overwriting of multiple headers<br> |
| X-Personium-RequestKey<br> | RequestKey field value output in the event log<br> | Single-byte alphanumeric characters, hyphens ("-"), and underscores ("_")<br>Maximum of 128 characters<br> | No<br>       | Supported in V 1.1.7 and later<br>                                                                                           |

##### OData Common Request Header

| Header Name<br>   | Overview<br>                                                     | Effective Value<br>      | Required<br> | Notes<br>                                                                                          |
|:-- |:-- |:-- |:-- |:-- |
| Authorization<br> | Specifies authentication information in the OAuth 2.0 format<br> | Bearer {AccessToken}<br> | No<br>       | * Authentication tokens are the tokens acquired using the Authentication Token Acquisition API<br> |

##### OData Acquire List Request Header

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

##### Common Response Header

| Header Name<br>                 | Overview<br>                                     | Notes<br>                                          |
|:-- |:-- |:-- |
| X-Personium-Version<br>         | API version that the request is processed<br>    | Version of the API used to process the request<br> |
| Access-Control-Allow-Origin<br> | Cross domain communication permission header<br> | Return value fixed to "*"<br>                      |

##### OData Response Header

| Item Name<br>          | Overview<br>                      | Notes<br> |
|:-- |:-- |:-- |
| Content-Type<br>       | Format of data to be returned<br> | <br>      |
| DataServiceVersion<br> | OData version information<br>     | <br>      |

#### Response Body

##### OData \$links Response body

The response is a JSON object, the correspondence between the key (name) and type defined in the object (subobject) and the value are as follows

| Object<br> | Name(Key)<br> | Type<br>   | Value<br>                            |
|:-- |:-- |:-- |:-- |
| Root<br>   | d<br>         | object<br> | Object{1}<br>                        |
| {1}<br>    | results<br>   | array<br>  | Array object {2}<br>                 |
| {2}<br>    | _uri<br>      | string<br> | URI of the linked OData resource<br> |

#### Error Messages

Refer to [Error Message List](004_Error_Messages.html)

#### Response Sample

```JSON
{
   "d": {
    "results": [
      {
        "uri": "https://{UnitFQDN}/{CellName}/__ctl/Role(Name='{RoleName}',_Box.Name=null)"
      },
      {
        "uri": "https://{UnitFQDN}/{CellName}/__ctl/Role(Name='{RoleName}',_Box.Name='box1')"
      }
    ]
  }
}
```

<br>

### cURL Command

```sh
curl "https://{UnitFQDN}/{CellName}/{BoxName}/{CollectionName}/$metadata/EntityType(Name='{EntityTypeName}')/$links/_AssociationEnd" -X GET -i -H 'Authorization: Bearer {AccessToken}' -H 'Accept: application/json'
```

<br><br><br><br><br>

###### Copyright 2017 FUJITSU LIMITED