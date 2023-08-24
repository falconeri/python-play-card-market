# python-play-card-market
## Add new user
### POST http://localhost:3000/user
### Body
    {
        "username": "#username#",
        "email": "#email#",
        "country": "#country#",
        "role": "#admin_or_regular#",
        "password": "#password#"
    }

## Login to get auth token
### POST http://localhost:3002/login
### Body
    {
        "email": "#email#",
        "password": "#password#"
    }

## Get All Users
_Only admin can get all users_
### Header: Authorization:#auth_token#
### GET http://localhost:3000/user

## Get User
_Admin can get any user, regular user can get only himself_
### Header: Authorization:#auth_token#
### GET http://localhost:3000/user/#user_id#?page=#page#&per_page=#per_page#
### Params:
- page - the number on the page you want to get
- per_page - how many users show on a page

## Update User
_Admin can update any user, regular user can update only himself_
_username and country can be updated_
### Header: Authorization:#auth_token#
### PATCH http://localhost:3000/user/#user_id#

## Delete User
_Admin can delete any user, regular user can delete only himself_
### Header: Authorization:#auth_token#
### DELETE http://localhost:3000/user/#user_id#

# Functional requirements:
> Users should be able to create an account and login
 
> All the calls should be authenticated (except login and register)
 
> Implement two user roles with different permission levels: a regular user would only be
able to CRUD on their owned records and an admin would be able to CRUD all records
and users (including other admins)

> Each user can have only one collection of player cards (user is identified by an email)

> When the user is signed up, they should get a collection of 5 cards (the system should
generate the player cards automatically)
 
> The name of the players from the cards and eventually their skill level should be
generated by a 3rd party API at your choice. The connection to the external web service
must be done asynchronously

> Each player card has an initial value of 100 coins

> Each player has a budget of 500 coins to buy other cards

> When logged in, a user can see his/her information and the value of their collection:
username and country (can be edited), collection value (sum of player cards values)

> A player card has the following information: name, age, skill level and market value

> Users can add their cards to an internal exchange market

> When a user places a card on the market, they must set the asking price/value for that
player card. This value should be listed on the market. When another user buys this
player, they must bought it for this price

> Each user should be able to see all cards from the exchange market

> With each buy/sell, collection budgets are updated

> When a card is bought by another player, its value should be increased based on a
machine learning algorithm at your choice. Aim for a good accuracy score.

> The API will return all the info in the JSON format and will use a database to provide
data persistence (the usage of SQLite is discouraged)

> The API should be able to support pagination for all the endpoints that return a list of
elements

> Use REST clients like Postman, cURL, etc. to test the API

> Write unit tests (not integration tests) so you can reach at least 50% code coverage for
the developed application. Use mocks for external dependencies.

# User
## Properties
- id
- username
- email
- password
- country
- role
- budget

## Routes
- login
- register
- read
- update
- delete

# Card
## Properties
- id
- name
- age
- skill
- market_value
- user_id

# Exchange Market
## Properties
- id
- user_id
- card_id
- price

## Routes
- sell
- buy
- get
