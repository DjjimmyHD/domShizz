# Stretch Goal

## Understanding helper functions

> There are 2 tasks to complete.
It's ok to revisit them later in the curriculum.

#### TASK #1: _After_ reading the `createElement` function below, write up to 3 sentences DEFENDING **why** this pattern is better?


```js

/*
Example DOM Element Builder:
createElement('div', {attributes: {'class': 'big-text header'}})
*/
function createElement(tag = 'div', {attributes = {}, events = {}, contents = ''}) {
  const element = document.createElement(tag);

  // Set attributes
  Object.keys(attributes || {})
    .forEach(key => {
      element.setAttribute(key, attributes[key])
    })
  
  // Add events
  Object.keys(events || {})
    .forEach(key => {
      // remove 'on' prefix: so 'onClick' becomes 'click'
      key = key.replace(/^on/i, '').toLowerCase()
      element.addEventListener(key, events[key])
    })
  
  // Insert/Append contents
  if (typeof contents === 'object') {
    element.appendChild(contents)
  } else { // Note: element.innerHTML is dangerous - use textContent instead
    element.textContent = contents || ''
  }
  
  return element
}

```


#### TASK #2: Write one sentence describing each of the 3 `createElement` calls below:

```js

// 1. 
const headerDiv   = createElement('div', {
  attributes: {'class': 'jumbotron huge-text header'}, 
  contents: 'HELLO!'})

// 2. 
const button = createElement('button', {
  attributes: {'class': 'btn btn-success', style: 'margin: 20hw'}, 
  contents: 'Click Me!',
  events: {'click': e => alert('clicked!')}
})

// 3. 
const buttonGroup = createElement('button', {
  attributes: {'class': 'btn-group'}, 
  contents: button
})

document.body.appendChild(headerDiv)
document.body.appendChild(buttonGroup)

```

> Live example on CodePen: https://codepen.io/justsml/pen/mxOqbo?editors=0110
