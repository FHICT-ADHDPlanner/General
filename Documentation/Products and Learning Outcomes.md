# Products and Learning Outcomes
This document will showcase the different products I have made during this semester. This will also explain what part of the products cover the different outcomes.

## Table of Content

## Planner API microservice
The first product I have worked on for this project was the main API backend application that makes sure that tasks can be requested, saved and edited. The API contains Secure Access points, this was done as to not have user see other users tasks. 

These secure access points require authorization through Auth0 (which will be touched upon later in the Auth0 *add link* chapter). These access points are CRUD access points for data and are only meant to be accessed by authorized users. 

The decision was made to use CRUD instead of CRUA because of the nature of the service. It is not necessary to archive any data if the user wants to delete a task from their planner. Thus CRUD was used. 

#### Accessing the API
As the API is running on a seperate server, the endpoints are slightly different. In this case, the API endpoints will be:
> GET Task: http://86.92.40.132:1001/api/Task/{id}

> GET Tasks: http://86.92.40.132:1001/api/Task

> POST Task: http://86.92.40.132:1001/api/Task

> PUT Task: http://86.92.40.132:1001/api/Task/{id}

#### Demonstration
Here is a quick demonstration of the API. For demonstration purposes Postman was used. 

#### Outcomes
The product touches learning outcomes 1 and 2.


