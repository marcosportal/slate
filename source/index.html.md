---
title: API Reference URI Online Judge

language_tabs:
  - python

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

## General Considerations

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
    'authorization': "Bearer " + "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U",
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
    'authorization': "Bearer " + "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U",
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

# User Data

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
    'authorization': "Bearer " + "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U",
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
    'authorization': "Bearer " + "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U",
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

## Submitting Source Codes

> For submit a source code use this example of requisition:

```python
import json
import requests

url = "https://api.urionlinejudge.com.br/runs/submit"

headers = {
    'content-type': "application/json",
    'accept': "application/json",
    'authorization': "Bearer " + "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U",
}

source = """
#include <stdio.h>

int main() {
    int A, B, X;

    scanf("%d", &A);
    scanf("%d", &B);

    X=A+B;

    printf("X = %d\\n", X);

    return 0;
}
"""

data = {
    'user': ID,
    'problem': 1001,
    'language': 1,
    'source': source,
}

response = requests.request("POST", url, data=json.dumps(data), headers=headers)

print(response.text)

```

> This code, will return a JSON like this:

```json
{
  "run":
    {
      "id":10382855,
      "user":119433,
      "problem":1001,
      "language":1,
      "created":"2018-05-15T14:03:41+00:00"
    }
}
```

- It is possible to submit a source code on behalf of a user using a POST request to the url:</br>
**POST**: ```https://api.urionlinejudge.com.br/runs/submit```

<aside class="notice">
Authorization to submit source code through API requires special authorization granted by the URI Online Judge team! If need to contact our team, please send feedback by this link: https://www.urionlinejudge.com.br/judge/en/contact
</aside>

<aside class="warning">
If your application does not have permission, the following message error will be returned: You are not authorized to access that location.
</aside>

<aside class="notice">
For the post method to work you need to send the user ID, language ID the problem ID and source code.
</aside>

### Languages

- The IDs listed below are the languages that are possible through the API submit

ID  | Name       | Compiler                      | Additional Time |
--- |------------|-------------------------------|-----------------|
1   | C          | gcc 4.8.5, -O2                | +0s             |
2   | C++        | g++ 4.8.5, -std=c++11 -02 -lm | +0s             |
3   | Java 7     | OpenJDK 1.7.0                 | +2s             |
4   | Python 2   | Python 2.7.6                  | +1s             |
5   | Python 3   | Python 3.4.3                  | +1s             |
6   | Ruby       | ruby 2.3.0                    | +5s             |
7   | C#         | mono 5.4.0                    | +2s             |
8   | Scala      | scalac 2.11.8                 | +2s             |
10  | JavaScript | nodejs 8.4.0                  | +2s             |
11  | Java 8     | OpenJDK 1.8.0                 | +2s             |
12  | Go         | go 1.8.2                      | +2s             |
13  | PostgreSQL | psql 9.4.14                   | +0s             |
14  | C99        | gcc 4.8.5, -std=c99 -O2 -lm   | +0s             |
15  | Kotlin     | Kotlin 1.2.0                  | +2s             |
16  | C++17      | g++ 7.2.0, -std=c++17 -02 -lm | +0s             |

<aside class="notice">
The Scala, JavaScript and Go are in beta.
</aside>

### Problems
<aside class="notice">
Only SQL problems (category 9) receive requests containing the PostgreSQL language.
</aside>

<aside class="warning">
Requests with PostgreSQL language in problems that are not in category 9 returned the following error message: The requested problem does not accept SQL solutions.
</aside>

<aside class="warning">
Requests in different language of PostgreSQL in problems of category 9 returned the following error message:he request problem can only accept SQL solutions
</aside>

### Source Code

- You can submit a request by passing the source code directly to the source assignment, however, one must pay attention to use escapes in special characters of the python language.</br> Any doubt consult the documentation: ```https://docs.python.org/2.0/ref/strings.html```

- If it is necessary to read the source code of an external file and then make the requisition, the example on the side shows how to do this.

<aside class="warning">
If you do not enter the source parameter in data, the following error message is returned: Source code should not be empty.
</aside>

> Requisition example of how to submit a source code from a file:

```python
import json
import requests

url = "https://api.urionlinejudge.com.br/runs/submit"

headers = {
    'content-type': "application/json",
    'accept': "application/json",
    'authorization': "Bearer " + "fyJ0eXPoOiLKO1QiiJIUzO1NiJ9.eyJzdWIiOjF9.5_KOZGatI2yINbYIBipBvFkDEtBiPqVEC-U",
}

PATH_TO_FILE = "/home/user/1001.c"

temp_file = open(PATH_TO_FILE,"r")

source = temp_file.read()

data = {
    'user': 119433,
    'problem': 1001,
    'language': 1,
    'source': source,
}


response = requests.request("POST", url, data=json.dumps(data), headers=headers)

print(response.text)
```