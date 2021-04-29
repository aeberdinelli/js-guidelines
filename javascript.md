Welcome to my set of a few good practice guidelines for JS. There are a few more on this repo for other kind of stacks, and I will soon create a set of rules for eslint to validate them.
# Guidelines for JS {
## General rules
- Always use `;` at the end of each command
- Always include spaces between brackets: `import { Thing, OtherThing } from './stuff';`
- Always declare arrays in single line when it has only a few elements: `[ 'thing', 'thing2' ];`
- Keep your code easy to understand, if you're using ternary operators, use it only for one condition, do not chain them

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
# };
