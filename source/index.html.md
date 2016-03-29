---
title: LMS API and Rabbitmq Docs

language_tabs:
  - shell

search: true
---

# Introduction

Welcome to the LMS API! You can use our API to access LMS API endpoints, which can get information on various courses, students, questions and lessons in our database.

# API Endpoints 

## Get All Questions and Lessons

> To get all questions and lessons, use this code

```shell
# Either call the questions endpoint
curl "http://example.com/api/v1/questions"

# Or call the lesson endponit to get all questions and lessons
curl "http://example.com/api/v1/lessons"
```
> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all questions and lessons.

### HTTP Request

`GET http://example.com/api/v1/lessons`

`GET http://example.com/api/v1/questions`

## Get a Specific Question 

```shell
curl "http://example.com/api/v1/questions/2"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific question.

### HTTP Request

`GET http://example.com/api/v1/questions/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the question to retrieve

## Get a Specific Lesson 

```shell
curl "http://example.com/api/v1/lessons/2"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific lesson.

### HTTP Request

`GET http://example.com/api/v1/lessons/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the lesson to retrieve

## Get All Courses

> To get all courses, use this code

```shell
curl "http://example.com/api/v1/courses"
```
> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all courses.

### HTTP Request

`GET http://example.com/api/v1/courses`

## Get a Specific Course 

```shell
curl "http://example.com/api/v1/course/2"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific course.

### HTTP Request

`GET http://example.com/api/v1/courses/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the course to retrieve

## Check User 

```shell
curl "http://example.com/api/v1/students/check"
    -H "username=someuser&password=somepassword"
```

> The above command returns JSON structured like this:

```json
{
  "success": true 
}
```

This endpoint checks if a specific user exists.

### HTTP Request

`POST http://example.com/api/v1/students/check`

### URL Parameters

Parameter | Description
--------- | -----------
username | The username of the student
password | The password of the student

# Rabbitmq Calls

## Get User Data 

> The call made from the sls to lms contains the email of the student

> The format of the the call is

```json
{
  "user_name": "someusername"
}
```

### Action Performed

The service on the lms side gets the student data as per the email address and sends that data in json format to the sls

## Save Analytics

> Sls sends student performance data over the rabbitmq to the lms

> The format of the call is

```json
{
  "question_id": 1,
  "student_id": 2,
  "course_id": 3,
  "option_id": 4
}
```

### Action Performed

The service written on the lms side retrives the data and saves the data in the database for future reference and also for providing visual analytics on the lms.

