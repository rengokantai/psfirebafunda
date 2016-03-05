#### psfirebafunda
#####3
```js
var fireRoot = "http://rengo.firebaseio.com/rootProj/";
userRef = new Firebase(fireRoot + 'users');
userRef.on('value',function(snap){
  func(snap.val());  //get all values of snap(userRef)
})
```
