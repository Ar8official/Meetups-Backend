
# Meetups (Backend)

## Contents

- [About](#overview)
- [Setup](#setup)
- [Tech Stack](#stack)
- [Deployment](#deploy)
- [Needed Tools](tools)
- [Documentation](#documentation)

## About Project <a name = "overview"></a>
This is an app to create, join, find or manage meetings, reunions, conferences and other important events.
Uses the Google Maps API for picking location, registered users have CRUD access for events and much more.

A frontend app which consumes the API from this app can be found at the [meetups](https://meetups-nine.vercel.app/) website. 

The react frontend code built with next.js can be found on github [here](https://github.com/Ar8official/Meetups)


## Setup <a name = "setup"></a>

### Add environmental vars

Create a .env file in the main project folder and add your cloudinary info for image CRUD tasks in the format below.

```
HOST = 0.0.0.0
PORT=1337
CLOUDINARY_NAME = "xxxx"
CLOUDINARY_KEY = "xxxx"
CLOUDINARY_SECRET = "xxxx"

```

### Install Dependencies

In the root folder of this project. Run the following command in the terminal to install all necessary dependencies required for the project.

```zsh

npm install 

```

### Start the Server

In the project top level 'server' directory, the following script will run the app in development mode by initiating both the client and backend server:
To start the app, run the following command.

```bash

npm run develop
# or
yarn develop

```

Open [http://localhost:1337/admin](http://localhost:1337/admin) to access the CMS Backend


## Tech Stack <a name = "stack"></a>
The tech stack mainly comprises of PostgresQL as the database, react, and node.js and deployed to Heroku. 

## Deployment <a name = "deploy"></a>
The backend app is already deployed on Heroku [here](https://meetupsbackend.herokuapp.com/).  

## Needed Tools <a name = "tools"></a>

This is a nodejs backend built with StrapiCMS, so be sure to get that installed. Other requirements include free developer accounts from [Cloudinary](cloudinary.com) for handling picture uploads, [Heroku](https://www.heroku.com/) for cloud hosting, Postgres Database for backend database hosting, Mapbox and Google Maps API for geolocation.


## Documentation <a name = "documentation"></a>

### JSON Objects returned by API:

Make sure the right content type like `Content-Type: application/json; charset=utf-8` is correctly returned.


#### User (Object Model)

```JSON
{
  "attributes": {
    "username": "tester",
    "email": "test@test.com",
    "password": "tyfughl",
    "role": {
      "model": "role",
      "via": "users",
      "configurable": false
    },
    "events": {
      "via": "user",
      "collection": "events"
    }
  }
}

```

#### Event

```JSON
  {
  	"name": "New event",
  	"slug": "new-event",
    "venue": "Villa Park",
    "address": "Villa Park, London ",
    "date": "22-10-2020",
    "time":"12:00PM",
    "performers": "VC",
    "description": "good event",
    "image": "file.png",
    "user": "tester"
}
```

#### Errors and Status Codes

If a request fails any validations, expect a 422 and errors in the following format:

```JSON
{
  "errors":{
    "body": [
      "can't be empty"
    ]
  }
}
```

##### Other status codes:

401 for Unauthorized requests, when a request requires authentication but it isn't provided

403 for Forbidden requests, when a request may be valid but the user doesn't have permissions to perform the action e.g "Insufficient credits.  Please add credits."

404 for Not found requests, when a resource can't be found to fulfill the request

### Event Endpoints:

#### View all events:

`GET "/events"`

No authentication required, returns a list of events

#### View all current user events

`GET "/events/me"`

Authentication required

#### Get the total number of events in the db

`GET /events/count"`

#### View a specific event given its id

`GET "/events/:id"`

No authentication required, returns an event

#### Create a new event

`POST "/events"`

Authentication required.

Required fields `name`, `venue`, `address`, `date`, `time`, `performers`, `description`

Optional field `image`

#### Update event with given id

`PUT "/events/:id"`

Authentication required. All fields are optional

#### Delete event with given id

`DELETE "/events/:id"`

Authentication required.     

