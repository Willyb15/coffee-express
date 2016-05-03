#DC Roasters Coffee Beans E-Commerce Site
##Built with Angular.js and Jade in Express.js
##Got Express up and running and put compass in there
```
express coffee
```
###Using index.jade + layout. jade began building content section
```jade
extends layout
block content
	.container-fluid.content
		.row
			.col-sm-12.coffee-cup-background
				//- img(src="images/coffee.jpg")
				.col-sm-12.coffee-cup-text
					h1 A Smarter way to Grind
					h4 Fresh Coffee Beans. 
					h4 Delivered to your door.
```

###Added Register and Login Routes in the index.js
```js
router.get('/register', function(req, res, next){
	res.render("register", {});
});
// POST
router.post('/register', function(req, res, next){
	// user posted: username, email, password, password2
	res.json(req.body);
	// res.render("register", {});
});
// Get route for the Login page
router.get('/login', function(req, res, next){
	res.render("login", {});
});
```

###Installed mongoose`
```
npm install mongoose --save
```
###Created mondels folder with accounts.js file
```js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;
var User = new Schema ({
	username: String, 
	password: String,
	emailAddress: String
});
module.exports = mongoose.model('User', User);
```


