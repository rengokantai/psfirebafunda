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

 
