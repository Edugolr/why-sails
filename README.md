# Why Sails.js
[![N|Solid](https://sailsjs.com/images/logos/sails-logo_ltBg_ltBlue.png)](https://nodesource.com/products/nsolid)
### About sails

#### What
Sails.js is a Realtime MVC backend framework for Node.js.
#### Who 
The Sails framework was developed by Mike McNeil to assist his team in building scalable Node.js projects for startup and enterprise customers. Since its release in 2012, Sails has become one of the most widely-used web application frameworks in the world.
#### Users
There are alot of big names using Sails.js, Im just gonna give you a few in this list and then you can check it out more if you want to at this link [Sails](https://sailsjs.com/)
 - [Microsoft](https://www.microsoft.com/en-us/)
 - [Verizon](https://www.verizonwireless.com/)
 - [Postman](https://www.getpostman.com/)
 - [American Eagle](https://www.ae.com/international?cm=sSE-cSEK)
 - [Philips](https://www.usa.philips.com/)
 

### Any database SQL/NoSQL ORM/ODM

Having the ability to seemlessly change between different databases I choose to build mine in MongoDb and use the built in document database for the testing. There is a long list of available database adapters 
- [Official](https://sailsjs.com/documentation/concepts/extending-sails/adapters/available-adapters#?officiallysupported-database-adapters)
- [Community](https://sailsjs.com/documentation/concepts/extending-sails/adapters/available-adapters#?communitysupported-database-adapters)

I found it very easy to switch between the databases and Im sure you will aswell. The only thing Ive had a hard time with was to make it work with SQLITE3, I managed eventuelly but it wasnt an easy setup like the rest of the databases.

Below is examples from my project, the first one where I implement MongoDb as the develop db
```
adapter: 'sails-mongo',
url: 'mongodb://root@localhost/chai17Ramverk2Proj'
```
And this one for testing
```
adapter: 'sails-disk',
```

### Auto-generated REST Api

This is a very powerful but slightly dangerous function. When I started to use Sails.js I did not know about this or how it worked, leaving my databse very open on all routes to read write and update as u please. However with knowledge comes power and with power great responsibility, or something alike. When you know about it and how it works, it is a great asset. 
Simply by using Sails CLI you can write

```
sails generate api User
```

This will create the Model: User and the Controller: UserController along with the RESTApi routes to handle the Model. 

- [add to](https://sailsjs.com/documentation/reference/blueprint-api/add-to)
- [create](https://sailsjs.com/documentation/reference/blueprint-api/create)
- [destroy](https://sailsjs.com/documentation/reference/blueprint-api/destroy)
- [find one](https://sailsjs.com/documentation/reference/blueprint-api/find-one)
- [find where](https://sailsjs.com/documentation/reference/blueprint-api/find-where)
- [populate where](https://sailsjs.com/documentation/reference/blueprint-api/populate-where)
- [remove from](https://sailsjs.com/documentation/reference/blueprint-api/remove-from)
- [update](https://sailsjs.com/documentation/reference/blueprint-api/update)

Model example, where attributes (or database columns if you like to look at it that way) has been added. 
```
//User Model

module.exports = {
    
    attributes: {
        firstname: {
            type: 'string',
            required: true
        },
        lastname: {
            type: 'string'
        },
        email: {
            type: 'string',
            isEmail: true,
            unique: true,
            required: true
        }
}
```


### Websocket integration

more magic coming up. Remember I told you about how things happened without me knowing it when I created my Model/Controller earlier. Well this happened aswell. How smooth is this ?
Simply make a get request on the route and you are hooked up on the websocket.
Simple as this,atleast most times:
Add a listener to the User model we created earlier.
```
io.socket.on('user', function(msg){
  console.log(msg);
})
```
Make a get request through io.socket.get on the route and you are subscribed.

```
io.socket.get('/user', function(resData) {
  console.log(resData);
});
```

Lets say someone would make a create on the Model User, then you would receive something like this in your log: 

```
{
    verb: 'created',
  id: 1,
  data: {
    id: 1,
    firstname: 'joe',
    lastname: 'Joesson',
    email: joejoe@email.com
    createdAt: '2014-08-01T05:50:19.855Z'
    updatedAt: '2014-08-01T05:50:19.855Z'
  }
}
```

How convenient, not only do you get the full info on the model, you also get what triggered the socket, in this case a create action.

## Author
[![Facebook](http://i.imgur.com/P3YfQoD.png)](https://www.facebook.com/christofer.wikman)
[![Github](http://i.imgur.com/0o48UoR.png)](https://github.com/Edugolr)
Christofer Wikman 



## Sources
- [Sails.js](https://sailsjs.com/)
- [Sitepoint](https://www.sitepoint.com/an-introduction-to-sails-js/)
- [Wikipedia](https://en.wikipedia.org/wiki/Sails.js)

