# Create Dynamic Search in Site API Design
 
## ***POST*** /V1/CMDB/Users
Call this API to create dynamic search in NetBrain Domain Management - Site Manager.
 
## Detail Information
 
> **Title** : Create Dynamic Search in Site API<br>
 
> **Version** : 07/11/2023
 
> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/Sites/Leaf/DynamicSearch
 
> **Authentication** :
 
|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token |

## Request body(****required***)
 
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|  |  | Need either or of siteId and sitePath. Calling this API to add dynamic search filter to the site which specified by site path or Id. All devices will be marked as manually added type. |
| sitesId^ | string | The unique id of specified site. |
| sitePath^ | string | Full path name of a site. For example, 'My Network/Site1/Boston'. |
| Dynamic filter | string | This string will include all parameters selected such as Device Property, Interface Property, Module Property, Config File, and Front Server, and their respective parameters. |

> ***Example***
 
 
```python
"expression" : "A and B",
  "conditions" : [{
    "schema" : "mainType", // the type of expression (e.g. A and B) should match with the type of the schema
    "operator" : 0, // range: 0~13
    "expression" : "",
    "escapeExpression" : false,
    "expressionNames" : null,
    "fieldType" : 0
   }, {
    "schema" : "intfs.speed",
    "operator" : 4,
    "expression" : "",
    "escapeExpression" : false,
    "expressionNames" : null,
    "fieldType" : 0
   }]
```
 
## Parameters(****required***)
 
>No parameters required.
 
## Headers
 
> **Data Format Headers**
 
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| Content-Type | string  | support "application/json" |
| Accept | string  | support "application/json" |
 
> **Authorization Headers**
 
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| token | string  | Authentication token, get from login API. |
 
## Response
 
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| statusCode | integer | The returned status code of executing the API. |
| statusDescription | string | The explanation of the status code. |
 
> ***Example***
 
 
```python
{
    'statusCode': 790200,
    'statusDescription': 'Success'
}
```
 
# Full Example:
 
 
```python
# import python modules
import requests
import time
import urllib3
import pprint
import json
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)
 
# Set the request inputs
token = '684c4e42-833a-428d-a5c9-3f047f3d3a67'
nb_url = "http://192.168.28.79"
full_url = nb_url + "/ServicesAPI/API/V1/CMDB/Users/SyncExternalUsers"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token
 
body = {
        "externalServerType": [1, 2]
        }
 
try:
    response = requests.post(full_url, data = json.dumps(body), headers = headers, verify = False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Sync AD/LDAP Users failed! - " + str(response.text))
 
except Exception as e:
    print (str(e))
 
```
 
    {'statusCode': 790200, 'statusDescription': 'Success.'}
     
 
# cURL Code from Postman:
 
 
```python
curl --location 'https://nextgen-training.netbrain.com/ServicesAPI/API/V1/CMDB/Users/SyncExternalUsers' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'token: 684c4e42-833a-428d-a5c9-3f047f3d3a67' \
--data '{
    "externalServerType": [1, 2]
}'
```