<small>Welcome to my set of a few good practice guidelines for JS. There are a few more on this repo for other kind of stacks, and I will soon create a set of rules for eslint to validate them.</small>

<details>
   <summary>
       <strong>Table of contents</strong>
   </summary>
   <strong>{</strong>
   <br>
    
   * [General rules](#general-rules)
   * [Always prefer const](#always-prefer-const)
      * [Updating an array](#updating-an-array)
      * [Updating an object](#updating-an-object)
   * [Exports](#exports)
      * [Export only what you need](#export-only-what-you-need)
      * [Export named methods](#export-named-methods)
   * [Arrow functions](#arrow-functions)
   * [Null checks](#null-checks)
     * [Defaulting a value](#defaulting-a-value)
     * [Optional property operator](#using-the-new-optional-property-operator)
   * [Looping through arrays](#looping-through-arrays)
     * [Removing items based on condition](#removing-items-based-on-condition)
     * [Performing operation for each element](#performing-an-operation-for-each-element)
     * [Customizing elements](#customizing-each-element-of-the-array)
     * [Using certain items from array](#using-a-certain-item-from-array)
   * [Spread operator](#spread-operator)
   * [Conditions](#conditions)
     * [Do not use redundant checks](#do-not-use-redundant-checks)
     * [Redundant ternary operators](#this-applies-to-ternary-operators-as-well)
     * [Redundant function returns](#and-in-functions-too)
     * [Redundant else](#you-dont-need-else)
   * [Typescript](#typescript)
     * [Type everything!](#type-everything)
     * [Dynamic types](#dynamic-types)
   
   <strong>}</strong>
</details>

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

<h3>Using a certain item from array</h3>

If you know what items you have in an array and want to use them, for instance the result of a `.split()` operation, you can do something like this:

```javascript
// Instead of
const parts = fullname.split(' ');
const name = parts[0];
const lastname = parts[1];

// You can do
const [ name, lastname ] = fullname.split(' '); 
```


<h2>Spread operator</h2>

I know sometimes it looks fancy but if you need to grab 8 properties from a 10 properties object, then it's more convenient to just use the object instead of spreading each property from it:

```jsx
// Instead of doing
const { prop1, prop2, prop3, prop4, prop5, prop6, prop7, prop8, prop9, prop10, prop11, prop12 } = obj;

// Refence the object itself
<p>Name: {obj.prop1}</p>
<p>Lastname: {obj.prop2}</p>
```

Your code will look cleaner with a lot less lines while getting the same result.

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

<h2>Typescript</h2>

"The whole point of using JS is that I don't have to care about types". I know, most JS developers when first presented TS hate it for this reason. I can assure you, it will help you prevent a lot of common errors. There's no need to use it but if you do, here's some useful tips.

### Type everything!!
Types are not only useful to prevent errors and fail compilation if there's a typo somewhere. They're also extremely useful for new developers. You can define the interface of your API (and other things) and welcome new developers to your project.

```typescript
interface CreateUserRequest {
    name: string;
    lastname: string;
    age?: number;
}

// This way people just need to check CreateUserRequest interface to find out what properties you accept
// Also if the IDE supports it, they will get autocomplete to make the DX delightful.
export function CreateUser(body: CreateUserRequest) {
```

### Dynamic types
Most TS developers don't take full advantage of the features available. There are a lot of places where `any` should not be an option. Usually they use `any` when they want to reuse a method across different entities. But you don't need to do that!

```typescript
// ResponseType is dynamic and you can send TS what type you are expecting from the method
export function Request(userId: number): Response<ResponseType> {
    return { name: 'Alan' } as ResponseType;
}

// You use it like this:
type User = { name: string };

// response will be of type User and the IDE will get full autocomplete options too
const response = Request<User>(1);
```

# };
