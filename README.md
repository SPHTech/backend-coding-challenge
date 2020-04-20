# Backend Coding Challenge

## Introduction

You are to create a Backend API for a simple blog system.

You are encouraged to display any knowledge of clean architecture and design pattern in the development of your application.

## Score

|Criteria|Score|
|--------|-----|
|Clean code / Development|60%|
|Unit / Integration test|30%|
|Docker|10%|

## Requirement

1. We value a **clean**, **simple** working solution.
2. The application can be run in **Docker**(10%), candidate can provide `docker-compose.yml` and `start.sh` bash script at the root of the project, which should setup all relevant services/applications.
3. The solution to be written in Go Lang
4. Candidates must submit the project as a git repository(we encourage you to commit often with only related changes). Repository must avoid containing the words `sphtech` and `challenge`.
5. Having **unit/integration** tests is a must(30%).
6. As we run automated tests on your project, you must comply to the API requirement as stipulated below. You can assume Docker is already installed in the test machine.
7. Please provide README instruction to setup and run your application on **macos**. 

## Problem Statement

1. Must be a RESTful HTTP API listening to port `8080` (or you can use another port instead and describe in the README)
2. The API must implement 3 endpoints with path, method, request and response body as specified
    - One endpoint to create an article (see sample)
        - To create an article, the API client must provide a title, content and a author (see sample)
        - The API responds an object containing the status and article id

    - One endpoint to get an article by id (see sample)
        - An error response should be returned if a client tries to get an article which doesn't exist.

    - One endpoint to list all articles (see sample)

3. The request input should be validated before processing. The server should return proper error response in case validation fails.
4. A Database must be used (SQL or NoSQL). The DB installation & initialisation must be done in `start.sh`.
5. All responses must be in json format no matter in success or failure situations.

## Api Interface

You are expected to follow the API specification as follows. Your implementation should not have any deviations on the method, URI path, request and response body. Such alterations may cause our automated tests to fail.

### Task 1 - Create an article
- Method: `POST`
- Path: `/articles`
- Request Body:
```
{
    "title": "Hello World",
    "content": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.",
    "author": "John",
}
```
- Response Header: `HTTP 201`
- Response Body:
```
{
    "status": 201,
    "message": "Success",
    "data": {
      "id": <article_id>
    }
}
```
or
- Response Header: `HTTP <HTTP_CODE>`
- Response Body:
```
{
    "status": <HTTP_CODE>,
    "message": <ERROR_DESCRIPTION>,
    "data": null
}
```

### Task 2 - Get article by id
- Method: `GET`
- Path: `/articles/<article_id>`
- Response Header: `HTTP 200`
- Response Body:
```
{
    "status": 200,
    "message": "Success",
    "data": [
      {
        "id": <article_id>,
        "title":<article_title>,
        "content":<article_content>,
        "author":<article_author>,
      }
    ]
}
```
or
- Response Header: `HTTP <HTTP_CODE>`
- Response Body:
```
{
    "status": <HTTP_CODE>,
    "message": <ERROR_DESCRIPTION>,
    "data": null
}
```

### Task 3 - Get all article
- Method: `GET`
- Path: `/articles`
- Response Header: `HTTP 200`
- Response Body:
```
{
    "status": 200,
    "message": "Success",
    "data": [
      {
        "id": <article_id>,
        "title":<article_title>,
        "content":<article_content>,
        "author":<article_author>,
      },
      {
        "id": <article_id>,
        "title":<article_title>,
        "content":<article_content>,
        "author":<article_author>,
      }
    ]
}
```
or
- Response Header: `HTTP <HTTP_CODE>`
- Response Body:
```
{
    "status": <HTTP_CODE>,
    "message": <ERROR_DESCRIPTION>,
    "data": null
}
```
