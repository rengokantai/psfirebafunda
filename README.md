#### psfirebafunda
#####3
```js
var fireRoot = "http://rengo.firebaseio.com/rootProj/";
userRef = new Firebase(fireRoot + 'users');
userRef.on('value',function(snap){
  func(snap.val());  //get all values of snap(userRef)
})
```

#####4
######push to create data
in lieu of  new Date().toString()
```
Firebase.ServerValue.TIMESTAMP
```
==
#####5
######update
```
ref.update({count:(user.count||0)+1}, function(err){....
```
#####6 querying
######orderByKey limitToLast
```
ref.child('one').limitToLast(3)
```
#####7 indexing
add indexes
```
"one":{
  ".indexOn":["name"]
}
```
Add indexs in multi unknown level
```
"one":{
  "$userKey":{
    ".indexOn":["a","b"]
  }
}
```
######index orderByValue
```
".indexOn":".value"
```

#####8
######anoy auth
```
var ref = new Firebase(rootlevelpath)
ref.onAuth(function(authData){
if(!authData){
}else{

}
});

ref.authAnonymously(function(err, authData){
if(!authData){
}else{

}
});
```
######auth with email
```
ref.authWithPasword({email:'j@j.com',password:'j'},function(err,authData){if(err){console.warn(err)}else{}})
```
register a user (log in requires manually add some code)
```
ref.createUser({email:'',password:''},function(err,userData){
  ref.authWithPassword({email:email,password:password},function(err,authData){  //must log in manually
  }) 
})
```
log out
```
ref.unauth()();
```
using oauth
```
ref.authWithOAuthPopup('twitter',function(err,data){....
```
==
#####9
######intro
default a node read is false(not readable)
```
{
"rules":{
"one":{
"two":{
".read":true,
".write":false
}
}
}}
```
######using expressions
```
"two":{
".write":"!data.child('propname').exists()"
}
```
#####auth
restrict logged in users (auth is built-in var)
```
".write":"auth!==null"
```
restrict specific user:
```
"users":{"$userkey":{
".write":"auth.uid=== $userkey"
}
}
```

only admin is allowed:
```
".write":"root.child('one').child('two').child(auth.uid).child('isAdmin').val()==true"  //add a isAdmin prop
```
###### vars
```
parent()
child('name')
val()
exists()
child(path)
children([paths])
isNumber()
isString()
isBoolean()
length
beginsWith()
endsWith()
seplace(o,n)
toLowerCase()
toUpperCase()
matches()
```
######basic vali (newData is built-in var)
```
"two":{
 ".validate":"newData.isNumber() && newData.val().length<=10"
}
```
######other vali (to prevent other values)
```
"$other":{".validate":false}
```

 
