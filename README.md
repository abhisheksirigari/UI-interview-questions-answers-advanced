## What is memoization?
Memoization is a form of caching where the return value of a function is cached based on 
its parameters. If the parameter of that function is not changed, the cached version of 
the function is returned.

Let’s understand memoization, by converting a simple function to a memoized function:
**Note- Memoization is used for expensive function calls but in the following example, we are considering 
a simple function for understanding the concept of memoization better.
```javascript
Consider the following function:

function addTo256(num){
  return num + 256;
}

addTo256(20); // Returns 276
addTo256(40); // Returns 296
addTo256(20); // Returns 276
```
// In the code above, we have written a function that adds the parameter to 256 and returns it.
When we are calling the function addTo256 again with the same parameter (“20” in the case above), we are
computing the result again for the same parameter.
Computing the result with the same parameter again and again is not a big deal in the above case, but 
imagine if the function does some heavy duty work, then, computing the result again and again with the same parameter will lead to wastage of time.

This is where memoization comes in, by using memoization we can store(cache) the computed results based on the parameters. If the same parameter is used again while invoking the function, instead of computing the result, we directly return the stored (cached) value.

Let’s convert the above function addTo256, to a memoized function:
```javascript
function memoizedAddTo256(){
  var cache = {};

  return function(num){
    if(num in cache){
      console.log("cached value");
      return cache[num]

    }
    else{
      cache[num] = num + 256;
      return cache[num];
    }
  }
}

var memoizedFunc = memoizedAddTo256();

memoizedFunc(20); // Normal return
memoizedFunc(20); // Cached return
```
In the code above, if we run memoizedFunc function with the same parameter, instead of computing the result again, it returns the cached result.

**Note- Although using memoization saves time, it results in larger consumption of memory since we are storing all the computed results.


## Explain how we can use a class outside a module where it was defined?
Answer: Usually, when we define a class, it has scope only inside the module. Therefore, you cannot access it beyond the module.
```javascript
module School {
  class Student {
    constructor(name: string, email: string) { }
  }
  let john = new Student('John', 'john@gmail.com');
}

let ann = School.Student('Ann', 'ann@yahoo.com');
```
TypeScript
As you can see, the variable ann will return error given the class Student cannot be accessed. If you wish to access the class, then you need to use the export keyword in TypeScript.
```javascript
module School {
  export class Student {
    constructor(name: string, email: string) { }
  }
  let john = new Student('John', 'john@gmail.com');
}

let ann = new School.Student('Ann', 'ann@yahoo.com');
```
TypeScript
At this point, the variable will not give error as we have accessed the Student class outside the module with the help of export keyword in TypeScript.




