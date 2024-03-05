# Update Site Properties API Design
 
## ***PUT*** /V1/CMDB/Users
Call this API to update site properties in NetBrain Domain Management.
 
## Detail Information
 
> **Title** : Update Site Properties API<br>
 
> **Version** : 26/10/2023
 
> **API Server URL** : http(s)://IP address of NetBrain Web API Server/ServicesAPI/API/V1/CMDB/Sites/SiteInfo
 
> **Authentication** :
 
|**Type**|**In**|**Name**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
|Bearer Authentication| Headers | Authentication token |

## Request body(****required***)
 
|**Name**|**Type**|**Description**|
|------|------|------|
|<img width=100/>|<img width=100/>|<img width=500/>|
| Name  | string | Name of site properties |
| Region | string | Region of customer |
| Location/Address | string | Location/Address of customer |
| Employee Number | integer | Number of employees |
| Device Count | string | Number of device in site |
| Contact Name | string | Site admin contact name |
| Phone number | string | Site admin phone number |
| Email | string | Site admin email |
| Type | string | Site type. (Headquarter, Data Center, Regional Office, Disaster Recovery) |
| Description | string | Description of site |
| --- | --- | --- |
| Customized Information | object | Site customized information |
 
> ***Example***
 
 
```python
{
   "siteInfo": [
       {
           "siteId": "1da4fda8-5d04-491b-8bb0-2e9abb989a60",
           "sitePath": "My Network/NA/US",
           "isContainer": true,
           "siteType": 0,
           "properties": {
               "name": "site1",
               "region": "XXXX",
               "locAdr": "Boston",
               "employeeNum": 1,
               "deviceNum": 50,
               "contactName": "XXXXX",
               "phone": "123456789",
               "email": "XXXX@.com",
               "siteType": "Headquarter",
               "description": "random example",
               "customizedInfo": [
                   "Field1": "XXXXXXXXXXXXXXXXXXXX",
                   .
                   .
                   .
                   ]         
             }
       },
       .
       .
       .
   ]
}
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