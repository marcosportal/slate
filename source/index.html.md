---
title: API Reference URI Online Judge

language_tabs:
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the official URI Online Judge API!

By harnessing the power of our API you can access information about our problems and build complementary tools to help the programming community.

## Getting Started

In order to request access to the URI Online Judge API, you must send feedback to our team containing the following information:

- Project details;
- Reason for using the UOJ API in your project;
- Estimated use. 
 
- To send the feedback with the request, use the link below:</br> ```https://www.urionlinejudge.com.br/judge/en/contact```
 
 **After submitting the request, the URI Online Judge team will contact you.**

## General considerations

- API endpoint:</br>```https://api.urionlinejudge.com.br```

### Requests

<aside class="success">
Important: Use HTTPS for all requests.
</aside>

- **By default, each site/application could make 100 requests per hour for the API endpoint.** This limit may be changed based on usage.

### Token authenticate

- To make requests to the API, you must obtain a TOKEN, that is **valid for 1 week**.

- Generated Token Example:</br>```fyJ0eXPoOiLKO1QiLCJhbGciOiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBiyDVmXIy2pBvFkDEtBiPqVEC-U```

<aside class="warning">
The token above is just an example, don't use this token in your application.
</aside>


### Timestamp

- Timestamps are rendered in ISO-8601 format: 2012-02-24T19:42:12+00:00

# Authentication

> To generate the access token, use the code:

```python
import json
import requests

url = "https://api.urionlinejudge.com.br/applications/token"

data = {
    'email': 'the-first-one@api.urionlinejudge.com.br',
    'password': '11uri12'
    }

headers = {
    'content-type': "application/json",
    'accept': "application/json",
    }

response = requests.request("POST", url, data=json.dumps(data), headers=headers)

print(response.text)
```

> Your Authorization token should look like this:

```json
{
  "token": "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U"
}
```

- Generate Token:</br>
**POST** ```applications/token```

<aside class="notice">
With this TOKEN, you can make GET requests, to get the categories and problems information.
</aside>

# Categories

> To access the categories use this code:

```python
import requests

url = "https://api.urionlinejudge.com.br/categories"

headers = {
    'content-type': "application/json",
    'accept': "application/json",
    'authorization': "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U",
    }

response = requests.request("GET", url, headers=headers)

print(response.text)
```

> This code, will return a JSON like this:

```json
{
  "categories": [
    {
      "id": 1,
      "problems": 188,
      "en": {
        "name": "Beginner"
      },
      "es": {
        "name": "Principiante"
      },
      "pt": {
        "name": "Iniciante"
      }
    },
    {
      "id": 2,
      "problems": 526,
      "en": {
        "name": "Ad-Hoc"
      },
      "es": {
        "name": "Ad-Hoc"
      },
      "pt": {
        "name": "Ad-Hoc"
      }
    },
  ]
}
```

- List categories:</br>
**GET:** ```/categories``` 

<aside class="success">
Remember to add an authentication header, with your token in your request!
</aside>

### JSON Return

Parameter  | Type    | Description
---------- | ------- | -------------------------------------------------
id         | integer | ID of the category
problems   | integer | Number of problems in this category
en         | object  | An object representing the English language
es         | object  | An object representing the Spanish language
pt         | object  | An object representing the Portuguese language

### Internationalized data

- The objects returned by the JSON of the categories, representing the languages, English, Spanish and Portuguese, return the following data.

Parameter | Type   | Description
--------- | ------ | -----------------------------------------------
name      | string | The name of the category according to the language

### Categories

ID | Category                      
---|-------------------------------
1  | Beginner                       
2  | Ad-Hoc                         
3  | String                         
4  | Data Structures and Libraries   
5  | Mathematics                    
6  | Paradigms                      
7  | Graph                          
8  | Computational Geometry                               

# Problems

> To obtain the information of the problems use this example of requisition:

```python
import requests

url = "https://api.urionlinejudge.com.br/problems/"

headers = {
    'content-type': "application/json",
    'accept': "application/json",
    'authorization': "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U",
    }

response = requests.request("GET", url, headers=headers)

print(response.text)
```

> This code, will return a JSON like this:

```json
{
  "problems": [
    {
      "id": 1001,
      "category": 1,
      "level": 1,
      "solved": 87353,
      "en": {
        "name": "Extremely Basic",
        "topics": "sequential"
      },
      "es": {
        "name": "Extremadamente Básico",
        "topics": "sequential"
      },
      "pt": {
        "name": "Extremamente Básico",
        "topics": "sequencial"
      }
    },
    {
      "id": 1002,
      "category": 1,
      "level": 1,
      "solved": 58115,
      "en": {
        "name": "Area of a Circle",
        "topics": "sequential"
      },
      "es": {
        "name": "Área del Círculo",
        "topics": "sequential"
      },
      "pt": {
        "name": "Área do Círculo",
        "topics": "sequencial"
      }
    },
  ]
}
```
- List Problems:</br>
**GET** ```/problems```

<aside class="success">
Remember to add an authentication header, with your token in your request!
</aside>

### JSON Return

Parameter  | Type    | Description
---------- | ------- | -------------------------------------------------
id         | integer | ID of problem
category   | integer | ID problem category
level      | integer | Level of the problem
solved     | integer | Number of the times that them problem was solved
en         | object  | An object representing the English language
es         | object  | An object representing the Spanish language
pt         | object  | An object representing the Portuguese language

### Internationalized data

- The objects returned by the JSON of the problems, representing the languages, English, Spanish and Portuguese, return the following data.

Parameter | Type   | Description
--------- | ------ | --------------------------------------------------------------
name      | string | The name of the category according to the language
topics    | string | Represent the subject of the problem according to the language

# User data

- It is also possible to obtain user profile information and list of submissions, but for this, it is necessary to obtain authorization from the user. Redirect, From your site/application to:</br>```https://www.urionlinejudge.com.br/judge/authorizations/app/NAME```

<aside class="notice">
The /NAME is given by the URI Online Judge team, based on the name of your application
</aside>

## Redirect

- After the user authenticates to the URI Online Judge (if it's not already logged in) and give permission, he will be redirected to the URL informed by you. You can pass the URL as a parameter, for instance:</br> ```https://www.urionlinejudge.com.br/judge/en/authorizations/app/NAME?redirect=https://www.yourapplication.com/uri/connect```

- Then, after the user authorized the application it would be redirected to (in this example):</br> ```https://www.yourapplication.com/uri/connect```

<aside class='notice'>
 That the redirect URL must be in https and must be from the same domain we have registered in our API, otherwise the default URL will be used in the redirect.
</aside>

### User parameter

- You can pass the user parameter in the redirect URL, so in this example you will get:</br> ```https://www.yourapplication.com/uri/connect?user=ID```

<aside class="notice">
After 5 users allowed access you must inform us and allow access to any member of our team to check the integration, allowing log in to the application seeking to ensure that all information is being handled securely and in accordance with the policies of our website (Which will be updated soon to reflect the uses of our API). Thus, the integration will be released to the other users.
</aside>

From this moment you can access:

## Profile

> To obtain the information of the user profile use this example of requisition:

```python
import requests

url = "https://api.urionlinejudge.com.br/users/profile/ID"

headers = {
    'content-type': "application/json",
    'accept': "application/json",
    'authorization': "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U",
    }

response = requests.request("GET", url, headers=headers)

print(response.text)
```

> This code, will return a JSON like this:

```json
{
  "user": {
    "id": 1,
    "name": "The Guardian",
    "statistics": {
      "rank": 12187,
      "solved": 56,
      "tried": 139,
      "submissions": 1336
    }
  }
}
```
- List user profile:</br>
**GET** ```/users/profile/ID```

<aside class="notice">
Where ID is the unique identifier of the user in the URI Online Judge.
</aside>

### JSON Return

Parameter               | Type    | Description
----------------------- | ------- | -------------------------------------
user                    | object  | An object representing the user
user[id]                | integer | Represent the user ID
user[name]              | string  | Represent the user name
statistics              | object  | An object representing the user statistics
statistics[rank]        | integer | Represents the user's rank
statistics[solved]      | integer | Represents how many problems the user has resolved
statistics[tried]       | integer | Represents how many problems the user tried to solve
statistics[Submissions] | integer | Represents how many submissions the user submitted

## Submissions

> For a list of user submissions use this example of requisition:

```python
import requests

url = "https://api.urionlinejudge.com.br/users/submissions/ID"

headers = {
    'content-type': "application/json",
    'accept': "application/json",
    'authorization': "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U",
    }

response = requests.request("GET", url, headers=headers)

print(response.text)

```

> This code, will return a JSON like this:

```json
{
  "runs": [
    {
      "id": 3,
      "problem": 1001,
      "answer": 1,
      "time": 0,
      "created": "2012-02-24T19:42:12+00:00"
    },
    {
      "id": 4,
      "problem": 1002,
      "answer": 6,
      "time": 0,
      "created": "2012-02-24T19:42:34+00:00"
    },
    {
      "id": 6,
      "problem": 1003,
      "answer": 5,
      "time": 0,
      "created": "2012-02-24T19:42:44+00:00"
    },
  ]
}
```

- List submissions:</br> 
 **GET**: ```/users/submissions/ID```

<aside class="notice">
Where ID is the unique identifier of the user in the URI Online Judge.
</aside>

### URL Parameters

Parameter | Values      | Description
------    | ----------- | ---------------
page      | Page number | Use for pagination
sort      | created     | Use to sort a submission by date created 
direction | asc OR desc | Use to sort in ascending or descending order

### Pagination

- Remembering that submissions are paginated. additional page information, if there is a next page or previous page, are returned along with the submissions, at the end.

- To access other pages just use this example:</br>
**GET**: ```/users/submissions/ID?page=2```

### Sorting 

- To sort the submissions by date created, you must use the **sort** in URL parameter.

- You can sort the result in ascending or descending order.

- To sort the submission just use this example:</br>
**GET**: ```/users/submissions/1?sort=created&direction=desc```


### JSON Return

Parameter  | Type    | Description
---------- | ------- | -------------------------------------
id         | integer | Submissions id
problem    | integer | Problem id
answer     | integer | Answer id
time       | integer | Time it took to judge the submission
created    | date    | Shows when this submission was judged

### Answers

Id  | Name                |  
--- |-------------------- |
0   | In Queue            | 
1   | Accept              | 
2   | Compilation Error   | 
3   | Runtime Error       | 
4   | Time Limit Exceeded | 
5   | Presentation Error  | 
6   | Wrong Answer        | 
9   | Closed              | 

- The descriptions of the answers can be accessed directly by the URL: [answers](https://www.urionlinejudge.com.br/judge/answers)

<aside class="notice">
You must be logged in to access this link
</aside>
