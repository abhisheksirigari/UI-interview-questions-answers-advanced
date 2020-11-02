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


## What is CI-CD and What are benefits of CI-CD ?
```javascrpt
Continuous Integration and continuous Delivery (CI/CD) is a set of software practices and techniques that enable the frequent release of small batches of code changes, with extensive visibility and traceability. It typically involves the creation of a largely automated pipeline that orchestrates the build, test and deployment of software across staged environments, ultimately leading to deployment in production.

benefits:
CI/CD offers several important benefits for development and test organizations:
Faster identification and resolution of defects : CI/CD allows an elegant way to establish the appropriate quality gates in the development and testing process. A fast feedback loop to the developers ensures that bugs are addressed early in the development cycle
Reduced overhead costReduced overhead cost Finding a bug at the development stage is the cheapest possible way to find it. If the same bug was to be fixed in any other environment, it would cost more. CI/CD requires some upfront overhead cost, but these are more than offset by the time and expense saved along the way.
Better quality assuranceBetter quality assurance CI/CD enables QA teams to release deployable software at any point in time. Without it, projects are prone to delayed releases because of unforeseen issues which arise at any point in the traditional development and test process.
Reduced assumptionsReduced assumptions CI/CD replaces testing assumptions with knowledge, thereby eliminating all cross-platform errors at the development stage.
Faster time to marketFaster time to market Faster test and QA cycles enable organizations to get quality products and services to market faster and more efficiently.
Software health measurabilitySoftware health measurability By establishing continuous testing into the automated integration process, software health attributes such as complexity can be tracked over time.
Better project visibility Frequent code integration provides the opportunity to identify trends in build success and failure and make informed decisions to address them. With CI/CD, dev and test teams can access real-time data on the code quality metrics to innovate new improvements and support decisions.
```

## One of your teammates accidentally deleted a branch, and has already pushed the changes to the central git repo. There are no other git repos, and none of your other teammates had a local copy. How would you recover this branch?
```javascript
answer: Check out the latest commit to this branch in the reflog, and then check it out as a new branch.
```

## How do you find a list of files that has changed in a particular commit?
```javascript
answer:
git diff-tree -r {hash}
Given the commit hash, this will list all the files that were changed or added in that commit. The -r flag makes the command list individual files, rather than collapsing them into root directory names only.

The output will also include some extra information, which can be easily suppressed by including a couple of flags:

git diff-tree --no-commit-id --name-only -r {hash}
Here --no-commit-id will supress the commit hashes from appearing in the output, and --name-only will only print the file names, instead of their paths.
```

## How do you squash last N commits into a single commit?
```javascript
answer:
Squashing multiple commits into a single commit will overwrite history, and should be done with caution. However, this is useful when working in feature branches. To squash the last N commits of the current branch, run the following command (with {N} replaced with the number of commits that you want to squash):

git rebase -i HEAD~{N}
Upon running this command, an editor will open with a list of these N commit messages, one per line. Each of these lines will begin with the word “pick”. Replacing “pick” with “squash” or “s” will tell Git to combine the commit with the commit before it. To combine all N commits into one, set every commit in the list to be squash except the first one. Upon exiting the editor, and if no conflict arises, git rebase will allow you to create a new commit message for the new combined commit.
```

## What is GitFlow?
```javascript
Git is a version control system. And GitFlow is a branching model of Git. People uses GitFlow for manage branches better and more logical.
Master
This is the live branch of the project. This is a production code. You need be careful when you commit this branch.
Hotfix
When you need to solve something in production code you can use Hotfix branch and open pull-request for master branch.
Develop
This branch same with master branch but you are using this branch for new feature developments. You can’t commit directly but it’s a better than use master branch. You clone this branch from master only one time. Same time you need merge hotfix to this branch.
Feature
Feature is the branch for the our new features on project. You clone new branch from development and start coding new features on this branch. After you will open pull-request on development branch and after that your code will be merged on development branch. But you need to be stay sync with development for avoid conflicts.
Release
When you finish all new feature development on dev branch you need test new features. You can create release branch and test changes before merge on production code. This environment named as a Staging. It means before production last chance to test everything.

BUT
GitFlow not solves all problem on branching. But it offers you a more logical branch structure. And this logical branch structure will provide a more efficient working environment over time.
```

## How would you check if a number is an integer?
```javascript
Answer
A very simply way to check if a number is a decimal or integer is to see if there is a remainder left when you divide by 1.

function isInt(num) {
  return num % 1 === 0;
}

console.log(isInt(4)); // true
console.log(isInt(12.2)); // false
console.log(isInt(0.3)); // false

```

## Given two strings, return true if they are anagrams of one another "Mary" is an anagram of "Army"
```javascript
var firstWord = "Mary";
var secondWord = "Army";

isAnagram(firstWord, secondWord); // true

function isAnagram(first, second) {
  // For case insensitivity, change both words to lowercase.
  var a = first.toLowerCase();
  var b = second.toLowerCase();

  // Sort the strings, and join the resulting array to a string. Compare the results
  a = a.split("").sort().join("");
  b = b.split("").sort().join("");

  return a === b;
}
```

## Create a function that will evaluate if a given expression has balanced parentheses -- Using stacks In this example, 
## we will only consider "{}" as valid parentheses {}{} would be considered balancing. {{{}} is not balanced
```javascript
var expression = "{{}}{}{}"
var expressionFalse = "{}{{}";

isBalanced(expression); // true
isBalanced(expressionFalse); // false
isBalanced(""); // true

function isBalanced(expression) {
  var checkString = expression;
  var stack = [];

  // If empty, parentheses are technically balanced
  if (checkString.length <= 0) return true;

  for (var i = 0; i < checkString.length; i++) {
    if(checkString[i] === '{') {
      stack.push(checkString[i]);
    } else if (checkString[i] === '}') {
      // Pop on an empty array is undefined
      if (stack.length > 0) {
        stack.pop();
      } else {
        return false;
      }
    }
  }

  // If the array is not empty, it is not balanced
  if (stack.pop()) return false;
  return true;
}
```



