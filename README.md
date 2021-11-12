<p align="center">
  <a href="" rel="noopener">
 <img width=200px src="favicon.png" alt="Project logo"></a>
</p>

<h3 align="center">Bookit</h3>

<div align="center">

[![Status](https://img.shields.io/badge/status-active-success.svg)]()

</div>

## About <a name = "about"></a>

A hotel booking app built react and node fullstack app using Next.js on React as the frontend, users can book rooms and pay with their credit cards, manage their bookings, download booking details as pdf and much more.

## Documentation <a name = "documentation"></a>

### JSON Objects returned by API:

Make sure the right content type like `Content-Type: application/json; charset=utf-8` is correctly returned.

#### Users (for authentication)

```JSON
{
  "user": {
    "name": "Borguuh",
    "email": "test@test.com",
    "token": "jwt.token.here",
    "image": "https://static.productionready.io/images/smiley-cyrus.jpg",
  }
}
```
#### User (Object Model)

```JSON
{
  "user": {
    "name": "jake",
    "email": "test@test.com",
    "avater": {
    	"url": "https://static.productionready.io/images/smiley-cyrus.jpg",
    	"public_id": "u1"
    },
    "role": "user"
  }
}
```

#### Place

```JSON
  {
    "name": "Charming Studio < 10 Miles to Wells' Beaches!",
    "pricePerNight": 168,
    "description": "A friendly atmosphere and natural delights await your visit to the town of Wells! Stay at this well-equipped 1-bath studio and enjoy easy access to several beaches, including Wells Beach and Drakes Island Beach, as well as Rachel Carson National Wildlife Refuge - the best spot for wildlife viewing just 8 miles away. Not to mention, with the downtown area just 10 minutes from the vacation rental,",
    "address": "4667 Bicetown Street, New York, NY, 10004",
    "guestCapacity": 1,
    "numOfBeds": 1,
    "internet": true,
    "breakfast": true,
    "airConditioned": false,
    "petsAllowed": false,
    "roomCleaning": true,
    "images": [
      {
        "public_id": "bookit/rooms/1_bzynlv",
        "url": "https://res.cloudinary.com/bookit/image/upload/v1618590762/bookit/rooms/1_bzynlv.jpg"
      },
      {
        "public_id": "bookit/rooms/2_s1u52n",
        "url": "https://res.cloudinary.com/bookit/image/upload/v1618590761/bookit/rooms/2_s1u52n.jpg"
      }
    ],
    "category": "King"
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

403 for Forbidden requests, when a request may be valid but the user doesn't have permissions to perform the action

404 for Not found requests, when a resource can't be found to fulfill the request

## User Endpoints:

#### Retrieve list of all users
`GET /api/admin/users`

Admin level authentication required, returns a list of all users


#### Get user details    

`GET /api/admin/users/:id`

Admin level authentication required, returns a specific user

#### Update user details 

`PATCH /api/admin/users/:id`

Example request body:
```JSON
{
  "user":{
    "name": "Jacob",
  }
}

```

#### Authentication:

`POST /api/users/login`

Example request body:
```JSON
{
  "user":{
    "email": "jake@jake.jake",
    "password": "jakejake"
  }
}
```

No authentication required, returns a [User](#users-for-authentication)

Required fields: `email`, `password`


#### Registration:

`POST /api/auth/register`

Example request body:
```JSON
{
  "user":{
    "name": "Jacob",
    "email": "jake@jake.jake",
    "password": "jakejake",
    "avatar": {
            "public_id": "result.public_id",
            "url": "result.secure_url"
        }
  }
}
```

#### Forgot Password:

`POST /api/password/forgot`

Example request body:
```JSON
{
  "user":{
    "email": "jake@jake.jake"
  }
}
```

No authentication required

Required fields: `email`

####Reset password  

`POST /api/password/reset/:token`

Example request body:
```JSON
{
  "user":{
    "password": "abcdef",
    "new_password": "abcdef"
  }
}
```
No authentication required


#### Get Current User

`GET /api/me`

Authentication required, returns current user


#### Update Current User

`PUT /api/me/update`

Example request body:

```JSON
{
  "user": {
    "name": "Jacob"
  }
}
```

Authentication required, returns a [User](#users-for-authentication)

Required fields: `email`, `username`



#### Delete user    

`DELETE   /api/admin/users/:id` 

Admin level authentication required


### Room Endpoints

#### Create room  

`POST /api/rooms`

Example request body:

```JSON
  {
    "name": "Charming Studio < 10 Miles to Wells' Beaches!",
    "pricePerNight": 168,
    "description": "A friendly atmosphere and natural delights await your visit to the town of Wells! Stay at this well-equipped 1-bath studio and enjoy easy access to several beaches, including Wells Beach and Drakes Island Beach, as well as Rachel Carson National Wildlife Refuge - the best spot for wildlife viewing just 8 miles away. Not to mention, with the downtown area just 10 minutes from the vacation rental,",
    "address": "4667 Bicetown Street, New York, NY, 10004",
    "guestCapacity": 1,
    "numOfBeds": 1,
    "internet": true,
    "breakfast": true,
    "airConditioned": false,
    "petsAllowed": false,
    "roomCleaning": true,
    "images": [
      {
        "public_id": "bookit/rooms/1_bzynlv",
        "url": "https://res.cloudinary.com/bookit/image/upload/v1618590762/bookit/rooms/1_bzynlv.jpg"
      },
      {
        "public_id": "bookit/rooms/2_s1u52n",
        "url": "https://res.cloudinary.com/bookit/image/upload/v1618590761/bookit/rooms/2_s1u52n.jpg"
      }
    ],
    "category": "King"
  }
```

Admin level authentication required, will return room

Required fields: all

#### Get room details   

`GET /api/rooms/:id`

No authentication required, returns a specified room

#### Update room details  

`PUT    /api/rooms/:id`

Example request body:

```JSON
{
  "name": "Charming Studio < 10 Miles to Wells' Beaches!"
}
```

Admin level authentication required, returns a [User](#users-for-authentication)

#### Create a new review   

`PUT    /api/reviews`

Example request body:

```JSON
{
  "user": "u1",
  "name": "Jacob",
  "rating": 5,
  "comment": "good room"

}
```

Authentication required, returns a [User](#users-for-authentication)



#### Delete room   

`DELETE  /api/rooms/:id` 

Admin level authentication required


### Payment Endpoints

#### Generate stripe checkout session   

`POST /api/checkout_session/:roomId`

Example request body:

```JSON
{
	"payment_method_types": "card",
	"success_url": "localhost:3000/bookings/me",
    "cancel_url": "{origin}/room/${room._id}",
    "customer_email": "test@test.com",
    "client_reference_id": "r1",
    "metadata": { 
    	"checkInDate": "2021-02-18",
    	"checkOutDate": "2021-02-20", 
    	"daysOfStay": 3 },
    "line_items": [
            {
                "name": "Charming Studio < 10 Miles to Wells' Beaches!",
                "images": [
				      {
				        "public_id": "bookit/rooms/1_bzynlv",
				        "url": "https://res.cloudinary.com/bookit/image/upload/v1618590762/bookit/rooms/1_bzynlv.jpg"
				      },
				      {
				        "public_id": "bookit/rooms/2_s1u52n",
				        "url": "https://res.cloudinary.com/bookit/image/upload/v1618590761/bookit/rooms/2_s1u52n.jpg"
				      }
				    ],
                "amount": 100,
                "currency": "usd",
                "quantity": 1
            }
        ]

}
```

## Create new booking after payment   

`POST /api/webhook`   

