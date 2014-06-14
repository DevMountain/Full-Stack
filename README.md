full-stack
=========

Now that you've created Applications with Angular and API's with Node and Express, let's combine them. The goal of this activity is to help you understand the 'big picture'. We're going to build an API using Node/Express, then we're going to build the interface (using Angular) that allows us to access our API. 

##Step 1: Setup your folder structure. 
* I don't want you to become too reliant on Yeoman. Everything we do today will be from scratch. 
* The important thing to understand is that now we're going to have both client side and server side code in the same directory. A common way to set up your folder structure for that is this way

```
public
  --> js
    --> app.js
    --> myCtrl.js
    --> myService.js
    --> myDirectives.js
  --> Styles
    --> style.css
  --> index.html
server-assets
  --> user.js
  --> login.js
server.js
```

Really note how that file structure is set up. We have a 'public' folder that holds our Angular or Front end app. We also have a server-assets folder that is going to hold anything that is a 'helper' to our server. Then we have our normal server.js file which will be where our API lives.

Go ahead and set up your file structure in the way above but leave the server-assets page blank.

##Step 2: Setup our API
By now you should have notice that Node uses a pretty cool module system for requiring files. Meaning, whenever you use code that looks like this 'var http = require('http')', node is going out and getting the http module and making it available to you. Well, we don't have to always rely on getting other peoples modules, we can also create our own and then require our own modules. This is a really powerful idea and allows our code to stay very modular and organized. 

If you remember using an Angular service, the only data that was available in our controller was the data we put on 'this'. It's the same idea with node. The only data that will be available when we require something is the data that we stick on 'module.exports'. This makes it really easy to have 'getter' and 'setter' methods to get and set our 'private' data. Here's an example. 

```javascript
var friends = ['Jake', 'Blaine', 'Travis'];
module.exports.getFriends = function(){
  return friends;
};

module.exports.addFriend = function(newFriend){
  friends.push(newFriend);
}
```
then in our server.js file we can do something like this

```javascript
var myFriends = require('./server-assets/pathToFriends');

myFriends.getFriends(); //returns our array of friends

myFriends.setFriends('Ben'); //adds Ben to our friends array
```

* Add a file to your server-assets called myData.js
* Fill that file up with the following 'private' information. 
* An array of objects that has each member in your family, their name, age, and relationship to you.
* An array of objects that has some of your closest friends, their name, age, and when you met them.
* An array of your favorite activities to do. 
* An object that has your name, height, age, favorite movie, favorite artist, and favorite food.

Now that we have our data...
* Now make getter and setter methods to be able to access each piece of Data in your file and be sure to put these getter and setter methods on 'module.exports' in order to be able to access them later in server.js once you require this file. 
