# User API Design

GET /V1/CMDB/Users{?username}&{?authenticationServer}
-----------------------------------------------------

Calling this API to get user information. If input username, API return just
this one user information. If no specific user name is input, API return all
user information.

Detail Information
------------------

>   **Title** : Get User(s) information API

>   **Version** : 19/03/2024.

>   **API Server URL** : http(s):// IP address of your NetBrain Web API Server
>   /ServicesAPI/API/V1/CMDB/Users

>   **Authentication** :

| **Type**              | **In**     | **Name**             |
|-----------------------|------------|----------------------|
|                       |            |                      |
| Bearer Authentication | Parameters | Authentication token |

Request body(\*\*\*\*required\*\*\*)
------------------------------------

>   No request body.

Query Parameters(\*\*\*\*required\*\*\*)
----------------------------------------

| **Name**             | **Type** | **Description**                                                                                                                                                           |
|----------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                      |          |                                                                                                                                                                           |
| username | string | The name of Netbrain system user. This field is the key to get the user information. if set "username" = null or "username" == "", API will returns all users information |
| authenticationServer^ | string   | The corresponding name of the authentication server |

**Note:** the "authenticationServer" is an optional attribute, to prevent
mis-retrieving if same user account names exist in different servers.
Check the detail in the following example.

Headers
-------

>   **Data Format Headers**

| **Name**     | **Type** | **Description**            |
|--------------|----------|----------------------------|
|              |          |                            |
| Content-Type | string   | support "application/json" |
| Accept       | string   | support "application/json" |

>   **Authorization Headers**

| **Name** | **Type** | **Description**                           |
|----------|----------|-------------------------------------------|
|          |          |                                           |
| token\*  | string   | Authentication token, get from login API. |

Response
--------

| **Name**                     | **Type**                     | **Description**                                                                                                                                                                                                                                                                                                                       |
|------------------------------|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                              |                              |                                                                                                                                                                                                                                                                                                                                       |
| UserData                     | list of object               | List of users info.                                                                                                                                                                                                                                                                                                                   |
| UserData.username            | string                       | The user name, this filed is the key to update the user information.                                                                                                                                                                                                                                                                  |
| UserData.email               | string                       | The email address of the user.                                                                                                                                                                                                                                                                                                        |
| UserData.firstName           | string                       | The first name of the user.                                                                                                                                                                                                                                                                                                           |
| UserData.lastName            | string                       | The last name of the user.                                                                                                                                                                                                                                                                                                            |
| UserData.allowChangePassword | bool                         | Decide whether to allow the user to change his/her password independently.                                                                                                                                                                                                                                                            |
| UserData.isSystemAdmin       | string                       | Decide whether to allocate the system administrator role to the user.                                                                                                                                                                                                                                                                 |
| UserData.isUserManager       | boolean                       | Decide whether to allocate the user manager role to the user.                                                                                                                                                                                                                                                                 |
| UserData.isSystemManager       | boolean                       | Decide whether to allocate the system manager role to the user.                                                                                                                                                                                                                                                                 |
| UserData.creationTime       | Time                       | Date and Time of creation                                                                                                                                                                                                                                                                 |
| UserData.lastUpdateTime       | Time                       | Date and Time of last update                                                                                                                                                                                                                                                                 |
| UserData.Status       | integer | Status of user accounts                                                                                                                                                                                                                                                                                                 |
|                              |                              | ▪ Active - 1                                                                                                                                                                                                                                                                             |
|                              |                              | ▪ Inactive - 2                                                                                                                                                                                                                                                                            |
|                              |                              | ▪ Pending - 3                                                                                                                                                                                                                                                                              |
|                              |                              | ▪ Deactivated - 4                                                                                                                                                                                                                                                                               |
|                              |                              | ▪ Unavailable - 5                                                                                                                                                                                                                                                                               |
| UserData.authenticationType  | int                          | The authentication type for the user account.                                                                                                                                                                                                                                                                                         |
|                              |                              | ▪ 1 - Local                                                                                                                                                                                                                                                                                                                           |
|                              |                              | ▪ 2 - External                                                                                                                                                                                                                                                                                                                        |
| UserData.phoneNumber         | string                       | The phone number of the user.                                                                                                                                                                                                                                                                                                         |
| UserData.department          | string                       | The department that the user belongs to.                                                                                                                                                                                                                                                                                              |
| UserData.description         | string                       | Any description about the user.                                                                                                                                                                                                                                                                                                       |
| UserData.deactivatedTime     | string                       | Specify the time when the user account is expired.                                                                                                                                                                                                                                                                                    |
| UserData.TenantAndRole       | list of TenantAndRole object | Specify Tenant And Role for the user.                                                                                                                                                                                                                                                                                                 |
|                              |                              | ▪ tenantId (string) - the ID of the tenant that the user can access.                                                                                                                                                                                                                                                                            |
|                              |                              | ▪ tenantName (string) - the name of the tenant that the user can access.                                                                                                                                                                                                                                                                            |
|                              |                              | ▪ isAdmin(bool) - decide whether to allocate the tenant administrator role to the user. If it is false, you need to specify a domain for the user to access.                                                                                                                                                                          |
|                              |                              | ▪ domains (list of objects) - the list of domains this user can access.                                                                                                                                                                                                                                                                            |
|                              |                              | ▪ canAddDomain(bool) - decide whether to allow the user to create domains.                                                                                                                                                                                                                                                            |
| users                        | list of object               | The list contains the dupilcate account information in different server.                                                                                                                                                                                                                                                              |
| users.authenticationServer   | string                       | The name of authentication server.                                                                                                                                                                                                                                                                                                    |
| users.userName               | string                       | The name of the user account.                                                                                                                                                                                                                                                                                                         |
| statusCode                   | integer                      | Code issued by NetBrain server indicating the execution result.                                                                                                                                                                                                                                                                       |
| statusDescription            | bool                         | The explanation of the status code.                                                                                                                                                                                                                                                                                                   |

>   **Example**

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# Normal Response:

{
  "UserData": [
    {
      "username": "Automation@Incident",
      "description": "Automation incident portal user for logins via access code.",
      "allowChangePassword": false,
      "isSystemAdmin": false,
      "isUserManager": false,
      "isSystemManager": false,
      "lastUpdateTime": "2022-03-14T18:23:27.185Z",
      "status": 1,
      "TenantAndRole": [
        {
          "tenantId": "22dc22dc-ab2d-cd8a-60a0-b6d667d61e4c",
          "tenantName": "Patch_Tenant",
          "isAdmin": false,
          "domains": [
            {
              "id": "7dd695d2-1990-40bf-bfd2-586f794a584c",
              "name": "Patch_Domain",
              "roles": [
                "Domain User",
                "Portal Temp User"
              ]
            },
            {
              "id": "833df35f-f550-4c9f-8fb0-c208834cf617",
              "name": "AutoBasicDomain",
              "roles": [
                "Domain User",
                "Portal Temp User"
              ]
            }
          ],
          "canAddDomain": false
        }
      ]
    },
    {
      "username": "NBPatchTester",
      "email": "aabc@netbraintech.com",
      "firstName": "test",
      "lastName": "patch",
      "allowChangePassword": false,
      "isSystemAdmin": true,
      "isUserManager": true,
      "isSystemManager": true,
      "creationTime": "2022-03-22T19:52:53.605Z",
      "lastUpdateTime": "2022-03-22T19:52:53.605Z",
      "status": 1,
      "TenantAndRole": [
        {
          "tenantId": "22dc22dc-ab2d-cd8a-60a0-b6d667d61e4c",
          "tenantName": "Patch_Tenant",
          "isAdmin": true,
          "domains": [
            {
              "id": "7dd695d2-1990-40bf-bfd2-586f794a584c",
              "name": "Patch_Domain",
              "roles": [
                "Domain Admin",
                "Domain User"
              ]
            }
          ],
          "canAddDomain": true
        },
        {
          "tenantId": "9c39e0a1-1f92-4fbd-9bab-c30f517f0f6c",
          "tenantName": "authTenant",
          "isAdmin": true,
          "domains": [],
          "canAddDomain": true
        }
      ]
    },
    {
      "username": "cheng",
      "email": "cheng@netbraintech.com",
      "firstName": "pu",
      "lastName": "cheng",
      "allowChangePassword": true,
      "isSystemAdmin": true,
      "isUserManager": true,
      "isSystemManager": true,
      "creationTime": "2022-03-25T15:49:10.554Z",
      "lastUpdateTime": "2022-03-25T15:49:10.555Z",
      "status": 1,
      "TenantAndRole": [
        {
          "tenantId": "22dc22dc-ab2d-cd8a-60a0-b6d667d61e4c",
          "tenantName": "Patch_Tenant",
          "isAdmin": true,
          "domains": [
            {
              "id": "7dd695d2-1990-40bf-bfd2-586f794a584c",
              "name": "Patch_Domain",
              "roles": [
                "Domain Admin",
                "Domain User"
              ]
            },
            {
              "id": "d4c69ed9-2220-4fc9-88cb-1472b4476a91",
              "name": "TableBasedDiagnosis",
              "roles": [
                "Domain Admin",
                "Domain User"
              ]
            }
          ],
          "canAddDomain": true
        },
        {
          "tenantId": "9c39e0a1-1f92-4fbd-9bab-c30f517f0f6c",
          "tenantName": "authTenant",
          "isAdmin": true,
          "domains": [],
          "canAddDomain": true
        }
      ]
    },
    {
      "username": "ydu",
      "email": "dsa@das.com",
      "firstName": "das",
      "lastName": "dsa",
      "allowChangePassword": false,
      "isSystemAdmin": true,
      "isUserManager": true,
      "isSystemManager": true,
      "creationTime": "2022-03-25T19:18:22.32Z",
      "lastUpdateTime": "2022-03-25T19:18:22.32Z",
      "status": 1,
      "TenantAndRole": [
        {
          "tenantId": "22dc22dc-ab2d-cd8a-60a0-b6d667d61e4c",
          "tenantName": "Patch_Tenant",
          "isAdmin": true,
          "domains": [
            {
              "id": "7dd695d2-1990-40bf-bfd2-586f794a584c",
              "name": "Patch_Domain",
              "roles": [
                "Domain Admin",
                "Domain User"
              ]
            }
          ],
          "canAddDomain": true
        },
        {
          "tenantId": "9c39e0a1-1f92-4fbd-9bab-c30f517f0f6c",
          "tenantName": "authTenant",
          "isAdmin": true,
          "domains": [],
          "canAddDomain": true
        }
      ]
    },
    {
      "username": "newuser",
      "email": "test@123.com",
      "firstName": "test",
      "lastName": "test",
      "phoneNumber": "",
      "allowChangePassword": false,
      "isSystemAdmin": false,
      "isUserManager": false,
      "isSystemManager": true,
      "creationTime": "2024-03-14T21:04:26.911Z",
      "lastUpdateTime": "2024-03-14T21:04:26.911Z",
      "status": 1,
      "TenantAndRole": [
        {
          "tenantId": "9c39e0a1-1f92-4fbd-9bab-c30f517f0f6c",
          "tenantName": "authTenant",
          "isAdmin": true,
          "domains": [],
          "canAddDomain": true
        }
      ]
    }
  ],
  "statusCode": 790200,
  "statusDescription": "Success."
}

# response with duplicate user accounts in different server without aunthentication server provided in input.
{
    "users": [
        {
            "authenticationServer": "NetBrain",
            "userName": "user1"
        },
        {
            "authenticationServer": "AD",
            "userName": "user1"
        }
    ],
    "statusCode": 792032,
    "statusDescription": "There are users with the same name 'user1' in the system,You need to specify the authentication server."
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Full Example:
=============

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
# import python modules 
import requests
import time
import urllib3
import pprint
import json
urllib3.disable_warnings(urllib3.exceptions.InsecureRequestWarning)

# Set the request inputs
token = "9eaef30e-3a21-44b7-8600-d21625a2198e"
nb_url = "http://192.168.31.191"
full_url = nb_url + "/ServicesAPI/API/V1/CMDB/Users"
headers = {'Content-Type': 'application/json', 'Accept': 'application/json'}
headers["Token"] = token

username = ""

data = {
        "username":username,
        "authenticationServer":"NetBrain"
    }

try:
    response = requests.get(full_url, params = data, headers = headers, verify = False)
    if response.status_code == 200:
        result = response.json()
        print (result)
    else:
        print ("Get Users Information failed! - " + str(response.text))
    
except Exception as e:
    print (str(e))  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
{
  "UserData": [
    {
      "username": "Automation@Incident",
      "description": "Automation incident portal user for logins via access code.",
      "allowChangePassword": false,
      "isSystemAdmin": false,
      "isUserManager": false,
      "isSystemManager": false,
      "lastUpdateTime": "2022-03-14T18:23:27.185Z",
      "status": 1,
      "TenantAndRole": [
        {
          "tenantId": "22dc22dc-ab2d-cd8a-60a0-b6d667d61e4c",
          "tenantName": "Patch_Tenant",
          "isAdmin": false,
          "domains": [
            {
              "id": "7dd695d2-1990-40bf-bfd2-586f794a584c",
              "name": "Patch_Domain",
              "roles": [
                "Domain User",
                "Portal Temp User"
              ]
            },
            {
              "id": "833df35f-f550-4c9f-8fb0-c208834cf617",
              "name": "AutoBasicDomain",
              "roles": [
                "Domain User",
                "Portal Temp User"
              ]
            }
          ],
          "canAddDomain": false
        }
      ]
    },
    {
      "username": "ydu",
      "email": "dsa@das.com",
      "firstName": "das",
      "lastName": "dsa",
      "allowChangePassword": false,
      "isSystemAdmin": true,
      "isUserManager": true,
      "isSystemManager": true,
      "creationTime": "2022-03-25T19:18:22.32Z",
      "lastUpdateTime": "2022-03-25T19:18:22.32Z",
      "status": 1,
      "TenantAndRole": [
        {
          "tenantId": "22dc22dc-ab2d-cd8a-60a0-b6d667d61e4c",
          "tenantName": "Patch_Tenant",
          "isAdmin": true,
          "domains": [
            {
              "id": "7dd695d2-1990-40bf-bfd2-586f794a584c",
              "name": "Patch_Domain",
              "roles": [
                "Domain Admin",
                "Domain User"
              ]
            }
          ],
          "canAddDomain": true
        },
        {
          "tenantId": "9c39e0a1-1f92-4fbd-9bab-c30f517f0f6c",
          "tenantName": "authTenant",
          "isAdmin": true,
          "domains": [],
          "canAddDomain": true
        }
      ]
    },
    {
      "username": "newuser",
      "email": "test@123.com",
      "firstName": "test",
      "lastName": "test",
      "phoneNumber": "",
      "allowChangePassword": false,
      "isSystemAdmin": false,
      "isUserManager": false,
      "isSystemManager": true,
      "creationTime": "2024-03-14T21:04:26.911Z",
      "lastUpdateTime": "2024-03-14T21:04:26.911Z",
      "status": 1,
      "TenantAndRole": [
        {
          "tenantId": "9c39e0a1-1f92-4fbd-9bab-c30f517f0f6c",
          "tenantName": "authTenant",
          "isAdmin": true,
          "domains": [],
          "canAddDomain": true
        }
      ]
    }
  ],
  "statusCode": 790200,
  "statusDescription": "Success."
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

cURL Code from Postman:
=======================

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
curl -X GET \
  'http://192.168.31.191/ServicesAPI/API/V1/CMDB/Users?username=&authenticationServer=NetBrain' \
  -H 'Accept: */*' \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Cache-Control: no-cache' \
  -H 'Connection: keep-alive' \
  -H 'Host: 192.168.28.173' \
  -H 'Postman-Token: 3cd9a344-50f6-4ae9-8c79-41a01f90ca41,e008e5f9-4fd7-4f2e-8e39-fd77d54d0651' \
  -H 'User-Agent: PostmanRuntime/7.15.2' \
  -H 'cache-control: no-cache' \
  -H 'token: b5bb9a78-f1e2-4a6a-bc67-d9ec18944ecd'
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Error Examples:
===============

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
###################################################################################################################    

"""Error 1: wrong inputs"""

Input:
    
        username = "kakakakaakak" # No user with a name called "kakakakaakak".
    
Response:
    
    "Get Users Information failed! - 
        {
            "statusCode":791006,
            "statusDescription":"user kakakakaakak does not exist."
        }"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
