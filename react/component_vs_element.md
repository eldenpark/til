### Component vs Element
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';

class MyComponent extends React.Component {
  constructor(props) {
    super(props);
    console.log('This is a component instance:', this);
  }

  render() {
    const another_element = <div>Hello, World!</div>;
    console.log('This is also an element:', another_element);
    return another_element;
  }
}

console.log('This is a component:', MyComponent)

const element = <MyComponent/>;

console.log('This is an element:', element);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

https://stackoverflow.com/a/42939845