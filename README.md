Welcome to my set of a few good practice guidelines for JS. There are a few more on this repo for other kind of stacks, and I will soon create a set of rules for eslint to validate them.
# Guidelines for JS {
## General rules
- Always use `;` at the end of each line
- Always include spaces between brackets: `import { Thing, OtherThing } from './stuff';`
- Always declare arrays in single line when it has only a few elements: `[ 'thing', 'thing2' ];`
- Keep your code easy to understand, if you're using ternary operators, use it only for one condition - **do not chain them**
- No matter what kind of indentation you use (spaces/tabs) as long as you use width of 4, this keeps the code clean and very easy to read
- Use spaces after each parameter in a function or method and between different parts of the declaration: `function something(param1, param2, param3) {`
- Use spaces to keep conditions and loops easy to read: `if (condition) {` / `for (let i = 0; i < 5; i++) {`

## Always prefer const
I prefer this for easy debugging and preventing errors. Remember, `const` means you cannot re-assign that variable, but you can change it's value if it is an array or an object.

<h3>Updating an array</h3>

```javascript
const rows = [];

// This is a React example, but it's valid for other cases too
people.forEach(person => {
    rows.push(
        <Row>
            <Col>{person.name}</Col>
        </Row>
    );
});
```

<h3>Updating an object</h3>

```javascript
const settings = {};

settings.darkMode = true;
```

## Exports
<h3>Export only what you need</h3>

If you have a module with the main method being something like `lowercase`, export only that method.

```javascript
function internal(str) {
    return str.toLowerCase();
}

function lowercase(str) {
    return internal(str);
}

// Do not export everything
module.exports = { internal, lowercase };

// Instead, export the useful methods
module.exports = { lowercase };
```

<h3>Export named methods</h3>
This also applies to classes. Is better to export a named method instead of a default export. This way, you will force everyone to use your method with the name that you specified and will make maintaince a lot easier, knowing exactly each place the exported method is used. Let me show you an example:

<br>

```javascript
// This is a default export
module.exports = function() {}

// This is a named export
function something() {}

module.exports = { something };

// Example for default export usage
// Both will work and they will have different name while they are the same method
const something = require('./something');
const notSomething = require('./something');

// This will make the method use the same name across your project (unless changing it on purpose)
// Plus instead of importing the whole module, you just import the method you need
const { something } = require('./something');
```

## Arrow functions?
I know, arrow functions are sexy. However, they are not always needed. Considerate using them only when:

- You need to maintain context for `this`
- You only have a single-line logic, like when using `.map()` or `.filter()` 

This will make also the previous rule easier to keep.

## Null checks
Always add nullchecks to prevent errors in your console and breaking the flow. <br />
You can use the falsy check or defaulting some value with the `||` operator. For example:

<h3>Defaulting a value</h3>

```javascript
const name = user.name || 'Unavailable';
```

<h3>Using the new optional property operator</h3>

```javascript
const name = user?.details?.name || 'Unavailable';
```

<br />
<h2>Looping through arrays</h2>
Try to not use the same iterator method everytime. Instead, use whichever is the better for your case.

<h3>Removing items based on condition</h3>

```javascript
const adults = people.filter(person => person.age >= 18);
```

<h3>Performing an operation for each element</h3>

Use `.forEach()` if you don't need to create a new array

```javascript
people.forEach(person => registerPerson(person));
```

<h3>Customizing each element of the array</h3>

In this case, you can use `.map()` since you need a new array with elements changed

```javascript
// This way you add new properties to array
const people = peopleArray.map(person => ({
    ...person,
    isAdult: (person.age >= 18)
});
```

<h2>Conditions</h2>

### Do not use redundant checks
If you have a condition that always returns either `true` or `false`, you don't need to compare it:

```javascript
// Do not use
if (something == true) {

// Instead just do
if (something) {
```

### This applies to ternary operators as well
```javascript
// Do not use
result = (condition != "") ? true : false;

// Just do this
result = (condition != "");
```

### And in functions too

```javascript
// Do not do this
function isSomethingTrue(something) {
    if (something) {
        return true;
    } else {
        return false;
    }
}

// Instead do this
function isSomethingTrue(something) {
    return (something);
}
```

### You don't need `else`
Sounds weird, but trust me your code will start to look a lot cleaner and easier to understand. <br />
You can use `return` or `throw` to stop the flow. 
There's a good article [right here ↗️](https://medium.com/@jamousgeorges/dont-use-else-66ee163deac3)  if you'd like to read more about this.

```javascript
function getName() {
    if (!person.name) {
        return 'Name not available';
    }
    
    return person.name;
}
```

# };
