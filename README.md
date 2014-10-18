full-stack
=========

Now that you've created Applications with Angular and API's with Node and Express, let's combine them. The goal of this activity is to help you understand the 'big picture'. You're going to build an API using Node/Express, then we're going to build the interface (using Angular) that allows you to access your API. 

##Step 1: Setup your folder structure. 
* Everything we do today will be from scratch. 
* The important thing to understand is that now we're going to have both client side and server side code in the same directory. A common way to set up your folder structure for that is like this...

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

Really note how that file structure is set up. We have a 'public' folder that holds our Angular or Front end code. We also have a server-assets folder that is going to hold anything that is a 'helper' to our server. Then we have our normal server.js file which will be where our API lives.

Go ahead and set up your file structure in the way above but leave the server-assets folder blank.

##Step 2: Setup our 'Server-Assets'
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

myFriends.addFriends('Ben'); //adds Ben to our friends array
```

* Add a file to your server-assets called myData.js
* Fill that file up with the following 'private' information. 
* An array of objects that has each member in your family, their name, age, and relationship to you.
* An array of objects that has some of your closest friends, their name, age, and when you met them.
* An array of your favorite activities to do. 
* An object that has your name, height, age, favorite movie, favorite artist, and favorite food.

Now that we have our data...
* Now make getter and setter methods to be able to access each piece of Data in your file and be sure to put these getter and setter methods on 'module.exports' in order to be able to access them later in server.js once you require this file. 
* Note your 'me' object will only have a GETTER not a SETTER.


##Step 3: Setup our API
Now that we have our server assets finished, let's go ahead and create our express API.
* Just like last class, create a very simple express server and test that it's working by sending back 'Hello World' whenever someone hits the index (/) of your app.
* Now, just like you can require other modules (http, express, body-parser), go ahead and require the server-assets module that is holding all your data. You do this by 'var myData = require('./server-assets/myData.js');'. Although you can just copy that line, really note what's going on and why the syntax is that way.
* Now, note that you're able to access all of the methods that you put on 'module.exports' to get your data.
* Now, create an API that allows you to GET and POST *ALL the data (besides your personal Object) from your server-assets data page. An example is below.
```javascript
app.get('/friends', function(req, res){
  var myFriends = myData.getFriends();
  res.send(myFriends);
});
```
* Check that your API is working using regular GET requests and POST requests with PostMan.

##Step 4: Create the Front End
Now that our API is complete, let's set up the front end to be able to display our data, in a beautiful way.
* Set up your 'public' folder to include all the files that are in the example file structure above (besides user.js and login.js). Remember to include each file in your index.html page or they won't work. 
* Test that your app is working by adding $scope.test = 'CSS IS AWESOME'; to your controller and then <p>{{test}}</p> to your index.html page, if everything is working move on, if not, check the console.
* In your index.html, create 4 buttons with each one retrieving and displaying different data from your API. ie. One button called 'Get Friends' that when you click it will run a function in your controller that gets your friends.
* Now that you have all your 'Getter' buttons set up, create 3 more buttons with corresponding input boxes that will accept input, then when the button is clicked it will run a function in your controller that will post the data that was in the input box to your API's POST method. Basically all your doing is allowing the front end to now post new data into your API.
* Now here's the part where it all fits together. Create an Angular service that, using $http, will go and retrieve your data you set up in your API. To wrap your head around this, just remember that all your API is saying is that when someone makes a get/post request to a certain URL, give that person back the data. So now on the front end, just make a get/post request to a certain url. ie. '$http({method: 'GET', url: '/friends'});
* Now that your index.html is set up and your service is set up, tie in all your functions in your controller to now go and use your service to retrieve your data from the API.
* 


<h4> This readme is intentionally very vague. Often times you'll have to work with documentation that is less than superior. Really try to see the bigger picture of what's going on in order to complete this assignment. </h4>
