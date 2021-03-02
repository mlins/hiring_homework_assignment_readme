# Zego/Mobile Doorman Homework Assignment

We designed this homework assignement as part of the hiring evaluation process at Zego/Mobile Doorman. Please send any questions to mlins@gozego.com

You can use whichever ruby framework/tools/gems (or no framework/tools/gems) that you feel comfortable with. Please design this in a way that you would for something that would go live into production (tests, docs, etc).

Create a *private* repository in github to host your code and give colloborater access to: https://github.com/mlins

# Goal

Write a ruby script to:
* make a GET request to https://test-users-2020.herokuapp.com/api/users
* send an Authorization Token with the value 'abc123' in the request headers
* parse the user json data returned, ignore invalid data, collate duplicate user data then write out transformed data to a json file

# Data

The data is an array of users where each user is similar to the following snippet
```
{
  "firstName": "Skipton",
  "lastName": "Waldemar",
  "email": "skipton@freda.gaither.com",
  "moreData": {
    "phone": "(856) 673-0305",
     "chrissie": "kelila"
  }
}
```
* In order for a user to be considered valid it must contain a `firstName`, `lastName` and either a valid `email` and or a valid `phone`. If not valid, ignore.

* A valid user is unique by its `firstName` and `lastName`.

* A phone number is valid if it contains exactly 10 numbers anywhere in the string.

# Transform
* Create a new list of the valid unique users sorted alphabetically by `lastName`.
* Format the phone numbers to be `(nnn) nnn-nnnn`.
* If  `phone` is present move it up a level.
* Collate the data.  For example if the following was found..
```  
{
  "firstName": "Tybalt",
  "lastName": "Loresz",
  "email": "tybalt@twelve.amby.com",
  "moreData": {
    "edaie": "lussier"
  }
},
.
.
.
{
  "firstName": "Tybalt",
  "lastName": "Loresz",
  "moreData": {
    "phone": "684 233--5122",
    "islaen": "maye"
  }
},
```
The transformed list would contain
```
{
  "firstName": "Tybalt",
  "lastName": "Loresz",
  "email": "tybalt@twelve.amby.com",
  "phone": "(684) 233-5122",
  "moreData": {
    "edaie": "lussier"
    "islaen": "maye"
  }
}
```

* Have the script write the transformed data out in json format to a file called `transformed.json` that can be read using a ruby `JSON.load('transformed.json')` call.
