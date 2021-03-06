# Captcha

Simple captcha for Connect/Express.

## Installation

Via npm:

	$ npm install express-captcha

## Usage (for Express 3)

```javascript
var express = require('express');
var captcha = require('express-captcha');

var app = express();

app.configure(function(){
    app.use(express.bodyParser());
	app.use(express.cookieParser());
	app.use(cookieSession({ secret: 'secretkeyhere' }));
	app.use(captcha({ url: '/captcha.jpg', color:'#000', background: '#f6f6f6' })); // captcha params
});

app.get('/', function(req, res){
	res.type('html');
	res.end('<img src="/captcha.jpg"/><form action="/login" method="post"><input type="text" name="digits"/></form>'); // captcha render
});

app.post('/login', function(req, res){
	res.type('html');
	res.end('CONFIRM: ' + (req.body.digits == req.session.captcha)); // captcha verify
});

app.listen(8000);
console.log('Web server started.');
```

## Full list of parameters
```javascript
    var params={
       "url":"/captcha.jpg",
       "color":"#ffffff",// can be omitted, default 'rgb(0,100,100)'
       "background":"#000000",// can be omitted, default 'rgb(255,200,150)'
       "lineWidth" : 2, // can be omitted, default 8
       "fontSize" : 40, // can be omitted, default 80
       "codeLength" : 6, // length of code, can be omitted, default 6
       "canvasWidth" : 150,// can be omitted, default 250
       "canvasHeight" : 100,// can be omitted, default 150
    }
    app.use(captcha(params)); // captcha params
```