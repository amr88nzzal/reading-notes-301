# Status Codes Based On REST Methods

*What is a HTTP Status Codes?*: A status code is a number higher than 100 and smaller than 600 that is part of a HTTP response. The first digit defines the class of the status. A status code comes with a reason phrase. The code is for programmatic recognition the phrase is for humans to understand what happened.

Learning how to read status can help you solve problems in your code quickly.

1. In your own words, describe what each group of status code represents:

    - 100’s = are **informational** status codes; telling the client request was received and is being processed.

    - 200’s = are **success codes**; telling the client request was accepted base on the requirements at the time of sending

    - 300’s = are **redirection** codes; telling the client that the resources they are looking for are not available right now. it can be temporary or permanent. The client needs to retry the request with new location

    - 400’s = are **client error** codes; telling the client that their requests to the server are invalid. Timeouts, wrong URI, missing authentication can cause this error. The client needs to put new input parameters before retrying the request.

    - 500’s = are **server error** codes; telling the client that the server is taxed, unable to be reach or the client request trigger error exceptions on the server. The client should try the request again.

*What is CRUD? (Create, Read, Update, Delete)*: regarding the four basic operations of persistent storage.

  **CRUD Table Example**: implemented via HTTPs methods

  | CRUD    | HTTP method   | Path        | Description     | Mongoose methods                    |
  |--------	|-------------	|-------------|----------------	|-------------------------------------|
  | Read   	| GET         	| `/cats`     | get all  cats  	| `Cat.find( )`                       |
  | Read   	| GET         	| `/cats/:id` | get one cat    	| `Cat.find({_id:id})`                |
  | Create 	| POST        	| `/cats`     | create one cat 	| `new Cat( )      .save( )`          |
  | Delete 	| DELETE      	| `/cats/:id` | Delete one cat 	| `Cat.findAndDelete`                 |
  | Update 	| PUT         	| `/cats/:id` | Update one cat 	| `Cat.find      (make changes).save` |
    
======

- Create: In the REASTful APIs use `POST` to create new resources or access tokens.
- Read: In the REASTful APIs use `GET` method use to fetch resource representations.
- Update: In the REASTful APIs use `PUT` method use to update or replace old with new resource
- Delete: In the REASTful APIs use `DELETE` method use to delete resource

2. What is a status code 202?

    * 202 ACCEPTED - used for asynchronous processing. This code tells the client that the request was valid, but its processing will finish sometime in the future.

    * indicates that the request has been accepted for processing, but the processing has not been completed. 

3. What is a status code 308?

    * 308 Permanent Redirect - this tells the client to use another URL to access the resource and not use the current URL anymore. 

4. What code would you use if an update didn’t return data to a client?

    * 204 No Content

5. What code would you use if a resource used to exist but no longer does?

    * 410 Gone

6. What is the ‘Forbidden’ status code?

    * 403 Forbidden

No Permissions: clients can’t access every resource on the backend, so we need a way to tell them about it
  - Statue Codes
    * 401 Unauthorized 
    * 403 Forbidden 

API Changes: when APIs change their structure
  - Status Codes
    * 307 Temporary Redirect
    * 308 Permanent Redirect

Errors: API frameworks use 500 and 404 status codes by default when something went wrong
  - Status Codes
    * 500 Internal Server Error
    * 404 Not Found

## Build a REST API with Node.js, Express, & MongoDB
  
1. Why do we need to pull our MongoDB database string out of our server and put it into our .env?
 
    - So when upload to github you don't send sensitive information to github. Which is public to everyone on the internet.

2. What is middleware?

    - runs between request and response cycle, access to next function of request-response life cycle
    
3. What does `app.use(express.json())` do?
  
    - allow our server to accept `json` has a body

4. What does the `/:id` mean in a route?

    - is a parameter that allows you to access with `request.params.id` the id of what was entered in

5. What is the difference between `PUT` and `PATCH`?

    - `PUT`: would update all the information of the user

    - `PATCH`: would update one part of information the user entered

6. How do you make a default value in a schema?

    - if info that need a require was not meet. The default will run `default:<default info>` 

7. What does a `500` error status code mean?

    - means there is an error status on your server

8. What is the difference between a status `200` and a status `201`?

    - `200`: you use status code `200` which means everything ok

    - `201`: when you send a post route you use status code `201` successful created