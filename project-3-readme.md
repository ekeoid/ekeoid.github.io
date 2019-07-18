# Chatter

**Chatter** is a app that helps you meet new people whereever you are. Anyone you see on Chatter is within a *configurable* 100 meters  of you and you won't see them when you leave. So when you talk to someone, introduce yourself and try to meetup with them! Seize the day!

This app has been built as part of the Full Stack Flex program under UNC Chapel Hill's Web Development BootCamp. This is is the final project for the program, which incorporates our final learning topic [React.js](https://reactjs.org/).

## Motivation
The idea of building **Chatter** was to build a service that wasn't just another chat application. Instead, this was meant to be a introductory *(a.k.a icebreaker)* for new people without much thought over the interaction. You could be at a bar, club, event, meeting, shopping or in the neighborhood and just need to make a *chatter*. This platform uses geolocation to assemble and filter people around you without any efforts of searching.

## Key Features (MVP)
Some of the main  features we wanted to implement for the project as part of the minimum viable product.
1. **User Authentication**: Users can register, login, and maintain persistent session
2. **Geolocation**: User location is trackable and accurate
3. **User Filtering**: Users are able to request, accept, decline, and ignore other users, which are all
4. **Private Chat**: USers that both accept to chat are allowed to enter a 1:1 conversation. 

## Technology Stack

### Front-end

* HTML5 / CSS3 / JavaScript
* React.js
* Bootstrap
* Material Design
* Axios
* Geolib
* Amazon Web Service S3

### Back-end

* Node.js
* Express.js
* MongoDB / Mongoose
* Socket.io
* Bcrypt

## Deployments
*Disclaimer: links may not be be active*
[Heroku Deployment](https://chatter-room-app.herokuapp.com/)
[Github Repository](https://github.com/lgfahys/project-3)


## Design

[Chatter Wireframe Prototype](https://share.proto.io/LS203K/)

##### User Authentication
- Nothing complex here. The signup form will take minimum required fields and a feature will allow the user to edit the thier profile to enter in additional information. 
- Password is secured using `bcrypt` as a hashing solution for the entered password. This feature is encapsulated in the model.
	```js
	userSchema.methods.generateHash = function(password) {
    	return bcrypt.hashSync(password, bcrypt.genSaltSync(8), null);
	};
	```
	```js
	userSchema.methods.validPassword = function(password) {
    	return bcrypt.compareSync(password, this.password);
	};
	```
- Session management was used to track user log ins. The `token` generated is based on the unique identifier of the `mongodb` key.

##### Geolocation
- Current position was based on the built-in browser API `Navigator`. Once location was obtained, the `geolib` library was used to identify target users with `getPerciseDistance()` and `isPointWithinRadius()`.

##### User Filtering
- Users are displayed on a main screen that renders users that are active to them, nearby based on geolocation, and pending requests that were either sent or recieved.
- Conditions will filter out display of the users across each user and update in mostly real-time, using `socket.io` to maintain communication across all connected users.
- There area that users can ge grouped: (1) Active Chats (2) Available and Within Location Range (3) User Pending action from you or to you.

- Conditions for available for chat:
  - User must be active
  - Users are within a certain radius of each other
  - User is not messaging with another user
  - Both users must accept invitation to be able to talk to each other
  - Activity flag (10 minutes) is available for the users

- Condition for not available for chat:
  - User is inActive
  - Exiting radius of the user
  - Leaving removes chat presence between users. 
  - A user decided to no longer continue conversation, end chat

##### Private Chat
- Chat function utilizes UI similar to Google Hangouts Messaging. Chat bubbles will be displayed for each user with the latest message at the botom.
- Room creataion happens automatically when a 2 users are created. This room identifier is the unique identifier for the `socket.io` room to maintain communication between the 2 users.

## App Overview

TBD


## How to try and use the app
You can fork the app or you can git-clone the app into your local machine. Once done that, please install all the dependencies by running 

`$ git clone https://github.com/lgfahys/project-3.git

`$ cd project-3`

Install project dependencies:

`$ npm install`

Start the app:

`$ npm start`


## Contributors

* [Lindsey Grayson Fahys](https://github.com/lgfahys/)
* [Elvin Eng](https://github.com/ekeoid)
* [Yevheniia Dilekoglu](https://github.com/yevheniia01)
* [Emert Ihegaranya](https://github.com/EmeryI)
* [Chase Vernon](https://github.com/csvernon)


# License
N/A
