Welcome to my style guidelines for React and JSX. There are (or will be?) other guidelines for other languages and libraries in this repository, feel free to visit them.
I will probably create an eslint rule set soon.

# Guidelines for React {
<h3>Creating class style element</h3>

```javascript
import React, { Component } from 'react';

export class Page extends Component {
    constructor() {
        super();
    }
    
    render() {
        return (
            <p>Things</p>
        );
    }
}
```

<br />
<h3>Returning simple element</h4>

```javascript
return (
    <Element />
);
```
<br />
<h3>Element with many props</h3>

```javascript
return (
    <Element
        prop1="something"
        prop2={something}
        prop3={`${something}-something`}
        prop4={false}
        style={{ margin: '5px' }}
    />
);
```

<br />
<h3>Element with child element in a prop</h3>

```javascript
return (
    <Element child={<Something />} />
);
```

<br />
<h3>Element with child element with many props on prop</h3>

```javascript
return (
    <Element 
        child={
            <Something 
                prop1="something"
                prop2="something"
                prop3="something"
            />
        } 
    />
);
```

<br />
<h3>Element with child with props and many props</h3>

```javascript
return (
    <Element 
        prop1="something"
        prop2="something"
        prop3="something"
        child={
            <Something 
                prop1="something"
                prop2="something"
                prop3="something"
            />
        } 
    />
);
```
# }
