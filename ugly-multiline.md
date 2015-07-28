## Code in question

* backend code in JavaScript run using node.js

```js
function findSomething(modelId, locationName) {
  var match = {
    state: locationName === 'National Average' ? {
      $exists: false
    } : locationName,
    model_id: modelId
  };
  
  return find(match);
}
```

## Why it is ugly?

* bad read experience, TODO describe criteria here
* how about code coverage measurement for ternary operators?

## Better code

```js
function findSomething(modelId, locationName) {
  var match = {
    state: locationName,
    model_id: modelId
  };
  
  if (locationName === 'National Average') {
    match.state = {
      $exists: false
    };
  }
  
  return find(match);
}
```

## Other issues with code in question

* `locationName === 'National Average'` shows frontend details leaked into backend
