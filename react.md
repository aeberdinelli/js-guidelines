Welcome to my style guidelines for React and JSX. There are (or will be?) other guidelines for other languages and libraries in this repository, feel free to visit them.
I will probably create an eslint rule set soon.

# Guidelines for React {
I prefer not using a default export, that way whenever you import a component, you make sure everyone is using the same name for that element. <br />
This means you won't have `import Something from './page';` and you will always have `import { Page } from './page';`
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
<h3>Function style element and hooks</h3>

```javascript
export function Page(props) {
    const [ title, setTitle ] = useState('Page title');
    
    return (
        <div className="page">
            <h1>{title}</h1>
        </div>
    );
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

<h2>Indentation</h2>
<h3>Do not use more than one level indent</h3>

```javascript
            <CardActions alignItems={'right'}>
                <ButtonComponent callback={props.filterBySelected}
                                text={'APPLY'}/>
                <ButtonComponent callback={() => setClearCheckbox(true)}
                                text={'CLEAR'}/>
            </CardActions>
```

<br />
<h3>Use just one instead</h3>

```javascript
<CardActions alignItems={'right'}>
    <ButtonComponent 
        callback={props.filterBySelected}
        text={'APPLY'}
    />
    <ButtonComponent 
        callback={() => setClearCheckbox(true)}
        text={'CLEAR'}
    />
</CardActions>
```
# }
