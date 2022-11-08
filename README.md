Original App Design Project - README Template
===

# WorkoutTracker

## Table of Contents
1. [Overview](#Overview)
1. [Product Spec](#Product-Spec)
1. [Wireframes](#Wireframes)
2. [Schema](#Schema)

## Overview
### Description
The WorkoutTracker app will allow users to create an account where they can login and see a list of workouts along with instructions on how to complete them and how many calories are burned with each workout. It can also keep track of which workouts are completed.

### App Evaluation
[Evaluation of your app across the following attributes]
- **Category:** Fitness
- **Mobile:** This app is designed to be used on mobile devices although it would be possible to expand the platform to allow users to view their data on other devices
- **Story:** Users to can create an account and view detailed instructions on how to complete specific workouts along with the ability to track their progress.
- **Market:** Any Individual interested in working out.
- **Habit:** This app as often or unoften as the user wants.
- **Scope:** First we would start with a predetermined list of workouts. Then we could potentially broaden the scope of the project to suggest workouts based on previous user activity.

## Product Spec

### 1. User Stories (Required and Optional)

**Required Must-have Stories**

* [1] User must have the ability to sign-in/create an account.
* [2] Upon login the user is presented with the main menu containing the following options: Account, Your Progreess, Workouts, Share, Logout.
* [3] User must have the ability to navigate between tabs (workouts/stats).
* [4] User can tap on a workout icon and transtion to the Workout Instructions page.
* [5] User can view the workout details on the instructions page and have the ability to mark the workout as completed.
* [6] Upon completing the workout the user is returned to workouts page.
* [7] User can view stats related to their account on the stats page.
* [8] User can navigate to an Account Details Page from the main menu.
* [9] User can view details such as Name and phone number from the Account Details Page.

**Optional Nice-to-have Stories**

* Ability to share progress to social media (ex: send out tweet)
* Take into account past workouts to recommend users new workouts.

### 2. Screen Archetypes

* Login Page
   * [1] User must have the ability to sign-in/create an account.
   * [2] Upon login the user is transitioned to a page with the list of workouts.
* Workouts Page
   * [3] User must have the ability to navigate between tabs (workouts/stats).
   * [4] User can tap on a workout icon and transtion to the Workout Instructions page.
* Workout Instructions Page
  * [5] User can view the workout details on the instructions page and have the ability to mark the workout as completed.
  * [6] Upon completing the workout the user is returned to workouts page.
* User Stats Page
  * [7] User can view stats related to their account on the stats page.
* Account Details Page
  * [8] User can navigate to an Account Details Page from the main menu.
  * [9] User can view details such as Name and phone number from the Account Details Page.
 
### 3. Navigation

**Tab Navigation** (Tab to Screen)

* Main Menu Tab
* Stats Tab

**Flow Navigation** (Screen to Screen)

* Forced Login Screen -> Main Menu Screen
* Main Menu Screen -> Workouts Screen
* Main Menu Screen -> Account Details Screen
 
## Wireframes
[Add picture of your hand sketched wireframes in this section]
<img src="https://i.imgur.com/6lSvOD4.jpg" width=600>

### [BONUS] Digital Wireframes & Mockups

### [BONUS] Interactive Prototype

## Schema 
### Models
#### Post

   | Property      | Type     | Description |
   | ------------- | -------- | ------------|
   | objectId      | String   | unique id for the user post (default field) |
   | author        | Pointer to User| image author |
   | image         | File     | image that user posts |
   | caption       | String   | image caption by author |
   | commentsCount | Number   | number of comments that has been posted to an image |
   | likesCount    | Number   | number of likes for the post |
   | createdAt     | DateTime | date when post is created (default field) |
   | updatedAt     | DateTime | date when post is last updated (default field) |
### Networking
#### List of network requests by screen
   - Home Feed Screen
      - (Read/GET) Query all posts where user is author
         ```swift
         let query = PFQuery(className:"Post")
         query.whereKey("author", equalTo: currentUser)
         query.order(byDescending: "createdAt")
         query.findObjectsInBackground { (posts: [PFObject]?, error: Error?) in
            if let error = error { 
               print(error.localizedDescription)
            } else if let posts = posts {
               print("Successfully retrieved \(posts.count) posts.")
           // TODO: Do something with posts...
            }
         }
         ```
      - (Create/POST) Create a new like on a post
      - (Delete) Delete existing like
      - (Create/POST) Create a new comment on a post
      - (Delete) Delete existing comment
   - Create Post Screen
      - (Create/POST) Create a new post object
   - Profile Screen
      - (Read/GET) Query logged in user object
      - (Update/PUT) Update user profile image
#### [OPTIONAL:] Existing API Endpoints
##### An API Of Ice And Fire
- Base URL - [http://www.anapioficeandfire.com/api](http://www.anapioficeandfire.com/api)

   HTTP Verb | Endpoint | Description
   ----------|----------|------------
    `GET`    | /characters | get all characters
    `GET`    | /characters/?name=name | return specific character by name
    `GET`    | /houses   | get all houses
    `GET`    | /houses/?name=name | return specific house by name

##### Game of Thrones API
- Base URL - [https://api.got.show/api](https://api.got.show/api)

   HTTP Verb | Endpoint | Description
   ----------|----------|------------
    `GET`    | /cities | gets all cities
    `GET`    | /cities/byId/:id | gets specific city by :id
    `GET`    | /continents | gets all continents
    `GET`    | /continents/byId/:id | gets specific continent by :id
    `GET`    | /regions | gets all regions
    `GET`    | /regions/byId/:id | gets specific region by :id
    `GET`    | /characters/paths/:name | gets a character's path with a given name
