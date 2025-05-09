
# Network Setting API Design

## ***PUT*** /V1/CMDB/NetworkSettings	
Call this API to enable the added account in network setting. The alias will be used as the key. 

Other parameters will be same as add network setting. They can be optional if no change occurs.

## Detail Information

> **Title** : Update Network Settings API<br>

> **Version** : 20/03/2024.

> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/NetworkSettings/TelnetInfo/EnableAccount

> **Authentication** : 

|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token | 

## Request body(****required***)

|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|telnetInfo* | object  | Used to add telnet/SSH login credentials. |
|telnetInfo.alias* | string  | The alias of telnet/SSH login credentials. This field is required. |


> ***Example***


```python
telnetInfo = {"alias" : "nb1111"}

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
|statusCode| integer | The returned status code of executing the API.  |
|statusDescription| string | The explanation of the status code.  |

> ***Example***


```python
{
    'statusCode': 790200, 
    'statusDescription': 'Success.'
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
token = "9c717c9a-4302-45b5-a068-2a3e9c4ea1a3"
nb_url = "http://192.168.28.79"
full_url = nb_url + "/ServicesAPI/API/V1/CMDB/NetworkSettings/TelnetInfo/EnableAccount"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

telnetInfo = {"alias" : "nb1111"}

try:
    response = requests.put(full_url, data=json.dumps(body), headers=headers, verify=False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Network settings update Failed! - " + str(response.text))

except Exception as e:
    print (str(e)) 
```

    {'statusCode': 790200, 'statusDescription': 'Success.'}
    

# cURL Code from Postman


```python
curl -X PUT \
  http://192.168.28.79/ServicesAPI/API/V1/CMDB/NetworkSettings \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: 55f96d7f-e2d7-479b-bd2a-7cccde000708' \
  -H 'cache-control: no-cache' \
  -H 'token: 9c717c9a-4302-45b5-a068-2a3e9c4ea1a3' \
  -d '{
        "privateKey" : 
            { 
                "alias" : "nopass23",
                "md5KeyContent" : "61e75483d397da0eda5a8dda67f13361",
                "keyContent" :   "8XmWX5It7yXvOw2J5UvziX@A==",
                "passwordPhrase" : "swed",
                "keyName" : "myRSA2048.ppk"

            },

        "telnetInfo" : 
            {
                "alias" : "nb23",
                "password" : "were2",
                "cliMode" : 0, 
                "keyName" : "",
                "userName" : "x22"

            },

        "privilegeInfo" : 
            {
                "alias" : "bj_office2",
                "password" : "2dEd",
                "userName" : "nl"
            },

        "snmpInfo" : 
            {
                "alias": "nb23",
                "snmpVersion": 3,

                "v3": 
                {
                    "userName": "peter",
                    "contextName": "peter_c",
                    "authMode": 2,
                    "authPro": 2,
                    "authPassword": "1"
                }
            },

        "jumpBox" : 
            {
                "alias": "nb3",
                "mode" : 1,
                "port" : 22,
                "ipAddr" : "10.10.5.141",
                "password" : "abc12356sd",
                "userName" : "pliu"
            }
    }'
```

# Error Examples:
Same with "Add Network Settings API"
