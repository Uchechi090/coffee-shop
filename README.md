# The Coffee Shop Project

This project is a digitally enabled coffee shop where students can order drinks, socialize, and study. The application: displays graphics representing the ratios of ingredients in each drink, allows the shop baristas to see the recipe information, allows public users to view drink names and graphics, allows the shop managers to create new drinks and edit existing drinks. As a part of the Fullstack Nanodegree, it served as an exercise module for lessons from Course 3: Identity Access Management. By completing this project, students learned and applied their skills to use Auth0 for authentication, authorization and practiced using Postman to test APIs.

All backend code follows [PEP8 style guidelines](https://www.python.org/dev/peps/pep-0008/). 

## Guidelines

At each stage, there are various TODOs marked. You'll also notice some TODOs in the frontend section. These have all been completed. 

You should feel free to expand on the project in any way you can.

## Getting Started

### Pre-requisites and Local Development 
Developers using this project should already have Python3, pip and node installed on their local machines.

#### Backend

From the backend folder run `pip install requirements.txt`. All required packages are included in the requirements file. The `.env.example` file contains the list of environment variables required by the project.

To run the application run the following commands: 
```
export FLASK_APP=api.py;
flask run --reload
```

These commands put the application in development and directs our application to use the `api.py` file in our src folder. Working in development mode shows an interactive debugger in the console and restarts the server whenever changes are made.

The application is run on `http://127.0.0.1:5000/` by default and is a proxy in the frontend configuration. 

#### Frontend

From the frontend folder, run the following commands to start the client: 
```
npm install // only once to install dependencies
```

#### Installing Ionic Cli

The Ionic Command Line Interface is required to serve and build the frontend. Instructions for installing the CLI is in the [Ionic Framework Docs](https://ionicframework.com/docs/installation/cli).

## Running Your Frontend in Dev Mode

Ionic ships with a useful development server which detects changes and transpiles as you work. The application is then accessible through the browser on a localhost port. To run the development server, cd into the `frontend` directory and run:

```bash
ionic serve
```

By default, the frontend will run on localhost:8100.

The Auth0 variables are added to the `environment.ts` file

## API Reference

### Getting Started
- Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, `http://127.0.0.1:5000/`, which is set as a proxy in the frontend configuration. 
- Authentication: This application uses Auth0 for its authentication/API keys. 

### Error Handling
Errors are returned as JSON objects in the following format:
```
{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
```
The API will return these error types when requests fail:
- 400: Bad Request
- 401: Unathorized
- 404: Resource Not Found
- 405: Method Not Allowed
- 422: Unprocessable
- 500: Internal Server Error

### Technologies used
- Python
- Flask
- SQLAlchemy
- Auth0
- PostgreSQL

### Models
There is only one data model used for the API, `Drink`.

### Drink
Entity representing a drink that can be ordered from the coffee shop.

#### Attributes:
- ``id``: unique integer id generated by postgres
- ``title``: Name of the drink
- ``recipe``: JSON array of a JSON object representing parts of the drink's recipe. Each ingredient of the recipe has these attributes:
  - ``color``: Color that the part will appear as on the web page
  - ``name``: Name of the ingredient
  - ``parts``: How much of the drink the ingredient makes up. For example: if ingredient ``A`` is 2 parts and the sum of the parts of all ingredients is 5 then the ingredient is 2/5 of the recipe
 
 #### Methods:
 - ``short()``: Returns a 'short' formatted representation of the drink. 
 - ``long()``: Returns a 'long' formatted representation of the drink. 
 - ``insert()``: Inserts the drink object into the SQL database.
 - ``delete()``: Deletes the drink object from the SQL database.
 - ``update()``: Updates the drink object in the SQL database.

### Endpoints
The endpoints can be found in `backend/src/api.py`.

- ``GET /drinks``: Gets all drinks in the short format returned by Drink class method ``short()``
- ``GET /drinks-detail``:  Gets all drinks in the long format returned by Drink class method ``long()``
  - Permission required: ``get:drinks-detail``
- ``POST /drinks``: Creates a new drink in the drinks table. 
  - Params required:
    - ``title``
    - ``recipe``
   - Permissions required: ``post:drinks``
- ``PATCH /drinks/<int:drink_id>``: Updates an existing drink model in the database. 
  - Arguments required: ``drink_id``, the id of the drink to be updated
  - Params required:
    - ``title``
    - ``recipe``
   - Permissions required: ``patch:drinks``
- ``DELETE /drinks/<int:drink_id>``: Deletes a drink from the database.
  - Arguments required: ``drink_id``
  - Permissions required: ``delete:drinks``

### Auth0
Auth0 is used to handle authorization of the API.

### Permissions
Here are the permisisons defined within Auth0 that the API uses:
- ``get:drink-details``: Read drink details
- ``post:drinks``: Create new drinks
- ``patch:drinks``: Edit drinks
- ``delete:drinks``: Remove drinks

### Roles
Two roles are defined that use different set of permissions.

#### Barista
Baristas only see the drinks and what ingredients are in them, so they only have one permission:
  - ``get:drinks``
  - ``get:drinks-detail``
  
#### Manager
The Manager has all the permissions:
- ``get:drink-details``
- ``post:drinks``
- ``patch:drinks``
- ``delete:drinks``

### Postman:
 
Exported collection with configured tokens can be found at: `/backend/udacity-fsnd-udaspicelatte.postman_collection.json`.

## Deployment N/A

## Authors
Yours truly, Uchechi Samuel

## Acknowledgements 
The awesome team at Udacity and all my fellow students!
