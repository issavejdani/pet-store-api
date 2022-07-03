- [Introduction](#introduction)
- [API integration process](#api-integration-process)
  * [Add a new pet](#post-add-a-new-pet)
  * [Find a pet by ID](#get-find-a-pet-by-id)
  * [Delete a pet by ID](#delete-delete-a-pet-by-id)
- [Sample Code](#sample-code)


# Introduction
 Petstore APIs were first designed and developed by [John Smith](#) as a hobby project. He created them on his weekends. One day he decided to make them open source by creating a public [repository](#) on Github. Then he used them to found a startup as they got bigger and bigger. This document will help you integrate the "pet" section of these APIs.
You can add, remove, and get a pet using these APIs.

# API integration process
Take a look at this [petstore.swagger.io](https://petstore.swagger.io) to start integrating these APIs. It gives you a lot of information at a glance. You can even test every API by clicking on "Try it out" button.

![try-out-button](https://user-images.githubusercontent.com/10261553/177050926-ae66f09c-5265-4aa1-bf7c-3e2c9b3fc46e.png)


## ```POST``` Add a new pet
|||
|-----|-----|
|Endpoint| /pet/|
|Sample url|https://petstore.swagger.io/v2/pet/|

### Input Parameters
|Name|Description|Required|Type|
|---|---|---|---|
|body|Pet object that needs to be added to the store|true|object|

### Example body 
```json
{
  "id": 0,
  "category": {
    "id": 0,
    "name": "string"
  },
  "name": "doggie",
  "photoUrls": [
    "string"
  ],
  "tags": [
    {
      "id": 0,
      "name": "string"
    }
  ],
  "status": "available"
}
```

### Response
|Status code|Response|
|---|---|
|200|``` {  "id": 9223372036854043000,  "category": {    "id": 0,    "name": "string"  },  "name": "doggie",  "photoUrls": [    "string"  ],  "tags": [    {      "id": 0,      "name": "string"    }  ],  "status": available"} ```
|405|Invalid Input|

## ```GET``` Find a pet by ID
|||
|-----|-----|
|Endpoint| /pet/{petId}|
|Sample url|https://petstore.swagger.io/v2/pet/3341|

### Input Parameters
|Name|Description|Required|Type|
|---|---|---|---|
|petId|ID of pet to return|true|string|


### Response
|Status code|Response|
|---|---|
|200|``` {  "id": 0,  "category": {    "id": 0,    "name": "string"  },  "name": "doggie",  "photoUrls":     "string"  ],  "tags": [    {      "id": 0,      "name": "string"    }  ],  "status": "available"} ```
|400|	Invalid ID supplied|
|400|	Pet not found|



## ```DELETE``` Delete a pet by ID
|||
|-----|-----|
|Endpoint| /pet/{petId}|
|Sample url|https://petstore.swagger.io/v2/pet/3341|

### Input Parameters
|Name|Description|Required|Type|Location|
|---|---|---|---|---|
|api_key|The key you need to authorize yourself|false|string|Header|
|petId|Pet id to delete|true|string|Querystring|

For this sample, you can use the api key ```special-key``` to test the authorization filters.


### Response
|Status code|Response|
|---|---|
|200|``` { "code": 200,"type": "unknown","message": "{petId}}"}```
|400|	Invalid ID supplied|
|400|	Pet not found|



# Sample Code
Using this piece of code in python, you can get a list of all pets base on their status. 
The status can be one of the followings:
- Available
- Pending
- Sold

This code returns a list of 10 pets with unique names and ```available``` status

## Setup and run
To run this code snippet, you need to install ```requests``` module by running the following command.
``` 
pip install requests 
``` 

Once you finish the installation process, save the code in a file named ```app.py``` and run it by running the following command.
``` 
python app.py 
```

```python
import requests

response = requests.get("https://petstore.swagger.io/v2/pet/findByStatus?status=available")
pets = response.json()
uniqueNames = []
i = 0


while (len(uniqueNames)<=9):
    if(pets[i]['name'] not in uniqueNames):
        uniqueNames.append(pets[i]['name'])
        print(pets[i]['id'] , pets[i]['name'])
    i = i + 1    
```