#DC Roasters Coffee Beans E-Commerce Site
##Built with Angular.js and Express.js
##Got Express up and running and put compass in there - See other readme's for full instruction on installing Express
```
express coffee blah blah blah
```
###Using index.jade + layout. jade + compass began building and styling Home Page
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
Blah Blah Blah
```
###Configured Routes in index.js to render a Redistration Page and Login Page
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
###Created Registration Page in register.jade our route points to
```jade
Blah Blah Blah
.row
	.col-sm-6.registration-form.text-center
		form(role="form", action="/register", method="post", id="registration-form", name="registration")
			.form-group
				label Username:
				input.form-control(type="text", name="username", placeholder="Will Bryant", minlength="5")
			.form-group
				label Password
				input.form-control(type="password", name="password", placeholder="6 character minimum", minlength="6")
Blah Blah BLah
```

###Installed mongoose`
```
npm install mongoose --save
```
###Configured Mongo and Mongoose in the index.js and Configure our DB and collection 
```js
var express = require('express');
var router = express.Router();
var mongoUrl = "mongodb://localhost27017/coffee"; // this will be the DB
var mongoose = require('mongoose');
var Account =require('../models/accounts');  //this is where we configure 
mogoose.connect(mongoUrl);
```
###Created mondels folder with accounts.js file
```js
var mongoose = require('mongoose');
var Schema = mongoose.Schema;

var Account = new Schema({
	username: String,
	password: String,
	emailAddress: String
});
module.exports = mongoose.model('Account', Account);
```
###Configured in index.js Post data to save to Database
```js
router.post('/register', function(req, res, next){
	//The user posted: username, email, password, password2
	if(req.body.password != req.body.password2){
		res.redirect('/register?failure=password');
	}
	var newAccount = new Account({
		username: req.body.username,
		password: req.body.password,
		emailAddress: req.body.email
	});
	console.log(newAccount);
	newAccount.save();
	res.json(req.body);
	// res.render('register', {})
});
```
####Redirect to Register Page if Passwords Don't Match
```js
if(req.body.password != req.body.password2){
	res.redirect('/register?failure=password');
}
```
```jade
.row
	if(failure)
		h2 You must enter same password in both fields!
	.col-sm-6.registration-form.text-center
		form(role="form", action="/register", method="post", id="registration-form", name="registration")
```
