### Work with Arrays in Javascript

#### Problem

You want to create, modify, iterate over, sort and manipulate arrays in Javascript

#### Assumptions
* [Node.js](https://nodejs.org/en/) is installed in your system

#### References
* 


***

#### Recipes

##### Define arrays

```javascript
let a = [];
let b = [1, 2, 3];
let c = [1, "q", 3];
c.length; // 3
```

##### Clone an array

```javascript
let d = c.slice(); // clone array
// WARNING!!
d = c; // "entangles" the two objects -- if you change one, the other changes
```

##### Manipulate arrays

```javascript
let a = ["sun", "mercury", "venus", "earth"]
a.reverse() // reverses 'a' in-place
```

##### Loop over an array

```javascript
let a = ["sun", "mercury", "venus", "earth"]
for (i in a) { console.log(i)} // --> 0, 1, 2, 3, 4 (indices)
for (i of a) { console.log(i)} // --> "sun", "mercury", "venus", "earth" (values)
a.forEach(i => console.log(i)) // --> "sun", "mercury", "venus", "earth" (values)
```

