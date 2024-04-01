# Assignment Four
## Purpose
The purpose of this assignment is to leverage Google’s analytics policies to gather information about the requests being sent in by users.

Using the information already entered to MongoDB for the previous assignment, you will add another collection of reviews that are tied to the movies. This way users can query the database and get the previous information (title, year released and actors) as well as the reviews. These two entities should remain separate! Do not append the reviews to the existing movie information.  

Leverage the Async.js library or mongo $lookup aggregation capability to join the entities.


## Requirements
- Create a collection in MongoDB (Mongo Atlas) to hold reviews about existing movies.
    - A review contains the name of the reviewer, a small quote about what they thought about the movie, and their rating out of five stars.
        - movieId (from the movie collection)
        - username
        - review
        - rating
    - The review collection should have at least one review for each movie. – The review can be a simple, ficticious review that you create.
- This API should build upon the previous API in assignment three.
    - If the user sends a response with the query parameter reviews=true, then the response should include the movie information as well as all the reviews for the movie. If they do not pass this in, the response should not show the reviews. – The review information should be appended to the response to the user.
        - Hint: Look at $lookup on how to aggregate two collections
    - Implement GET/POST (DELETE is optional for reviews)
        - POST needs to be secured with a JWT authorization token.  The Username in the token should be stored with the review (indicating the user that submitted the review)
            - If review created send back JSON message { message: 'Review created!' } 
- Extra Credit:  Add custom analytics to return information about which movies users are querying.
    - Create a custom analytics policy that describes the number of times each movie has been reviewed. To do this, you will have to send a number of requests for each movie.
        - Custom Dimension: Movie Name
        - Custom Metric: Requested:  Value 1 (it will aggregate)
    - Custom Dimension and Metric should be sent with an Event type 
        - Event Category: Genre of Movie (e.g. Western)
        - Event Action: Url Path (e.g. post /reviews)
        - Event Label: API Request for Movie Review
        - Event Value: 1 


## Submissions
- Create a Postman test to test your API. You should include the following requests.
    - All tests from HW3 and
    - Valid request without the review query parameter (e.g reviews=true on the /movies route)
    - Invalid request (for a movie not in the database) without the review query parameter. 
    - Valid request with the review query parameter. (e.g reviews=true on the /movies/:id route)
    - Valid save review method that associates a review with a movie (save a review for a movie in your DB)
    - Invalid save review (movie missing from DB)
    - Export a report from Google Analytics (only if you do the Extra Credit)

- Create a readme.md at the root of your github repository with the embedded (markdown) to your test collection
    - Within the collection click the (…), share collection -> Embed
    - Static Button
    - Click update link
    - Include your environment settings
    - Copy to clipboard 
- Submit the Url to canvas with the REPO CSC_3916
- Note: All tests should be testing against your Heroku or Render endpoint

## Rubic
- This one has an extra credit – code the custom analytics that correctly sends the movie name and they attach a PDF or Excel report from Google Analytics you receive +4
- -2 if missing reviews collection
- -2 if missing query parameters ?reviews=true that returns reviews (should include both movie and reviews)
- -1 for each test that is missing (valid request for movie with query parameter, valid save review, invalid movie request, invalid save review) – for max of (-4 for missing all tests)
- -2 if you have to manually copy the JWT token to get their tests to run (versus saving it from the sign-in call)
- Try changing the review data to enter a different review before submitting to validate new review are returned – if not (-1)

## Resources
- https://github.com/daxko/universal-ga
- https://developers.google.com/analytics/devguides/collection/analyticsjs/custom-dims-mets 
- https://cloud.google.com/appengine/docs/flexible/nodejs/integrating-with-analytics
- https://caolan.github.io/async/index.html
- https://support.google.com/analytics/answer/2709829


## Explanation of your project
- The project is an API designed for managing a movie database. It manages movies and reviews, both with additional objects of information. 


## Installation and usage instructions
- Run and Fork Postman
- Send the following requests in order: 
- 1) SignUp a User (accept) - creates a user
- 2) SignUp a User 2 (accept) - creates a second user
- 3) SignIn a User (accept) - signs in the first user created
- 4) Save movie 1 (accept) - saves a movie into the database
- 5) Save movie 2 (accept) - saves a movie into the database
- 6) Save movie 3 (accept) - saves a movie into the database
- 7) Save movie 4 (accept) - saves a movie into the database
- 8) Save movie 5 (accept) - saves a movie into the database
- 9) Save movie 6 (accept) - saves a movie into the database
- 10) Save movie 7 (accept) - saves a movie into the database
- 11) GET movies to get the IDs (accept) - gets the list of movies so you can use the movie id for other requests
- 12) Save review 1 (accept - using movie 7 Gladiator) - saves a review to the movie Gladiator using the movie id
- 13) Save review 2 (accept - using movie 7 Gladiator) - saves a review to the movie Gladiator using the movie id
- 14) Save review 1 (Error - No matching ID/movie missing from DB) - tries to save a review but the movie id is not existing
- 15) Save review 1 (Error -  Missing a required review field) - tries to save a review but the movie id is blank
- 16) GET movies without the review query parameter (Error -  movie not in the database) - tries to pull a movie but the movie id is not in the database 
- 17) GET movies without the review query parameter (Accept - one movie only) - pulls a movie successfully but without the reviews
- 18) GET movies with the review query parameter (accept) - pulls all of the movies and the reviews 
- 19) GET reviews to get the review ID (accept) - pulls only the reviews to get the review id to delete it in a different request
- 20) Delete review (accept) - deletes a review using the review id 


## Postman Link
[<img src="https://run.pstmn.io/button.svg" alt="Run In Postman" style="width: 128px; height: 32px;">](https://app.getpostman.com/run-collection/32601991-50b0cf9f-6059-450e-84fa-368f23053d5a?action=collection%2Ffork&source=rip_markdown&collection-url=entityId%3D32601991-50b0cf9f-6059-450e-84fa-368f23053d5a%26entityType%3Dcollection%26workspaceId%3Df70b2cfd-36ab-4105-adba-720513baa397#?env%5BTristenPerez-HW4%5D=W3sia2V5IjoiSldUIiwidmFsdWUiOiIiLCJlbmFibGVkIjp0cnVlLCJ0eXBlIjoiYW55Iiwic2Vzc2lvblZhbHVlIjoiSldULi4uIiwic2Vzc2lvbkluZGV4IjowfV0=)


## REACT Link
https://csc3916-react-pereztri-hw4.onrender.com


## The environment settings
- Postman collection name: CSCI3916_HW4
- Postman environment name: TristenPerez-HW4