# JS SDK

### Binding your state

Since your state and location is so important for your neighbours and you want to know what is around you, we provide functionality that will update exaQuark as frequently as required.  
All you need to do is provide a function that will return your [Entity State](entity-state.html).

For example:

```javascript
exaQuark.bind(getCurrentState)

// In your app, the getCurrentState will be something like this:

var getCurrentState = function () {
  return myState // where your state should be the same format as the specified in the {{EntityState}} documentation
}
```

If we don't receive an update from you for 30 seconds, we will close the connection.

### Sending updates

**Send some arbitary data directly to your neighborhood**

```javascript
exaQuark.push('signal:broadcast', {
  universeId: 'UNIVERSE_ID', 
  reach: 1, // 1 - 5 neighborhoodLevel
  signal: { } // data to be sent
})
```

**Send some arbitary data directly to one or more entity**

```javascript
// this can only reach a user within your current neighborhood
exaquark.push('signal:private', {
  universeId: 'UNIVERSE_ID',
  iids: [ {{ARRAY_OF_RECIPIENT_IIDS}} ]
  signal: { } // data to be sent
})
```

#### Force a state update

Sometime you want to immediately update your neighbors of changes \(such as when you teleport\). For this you can use the following function.

```javascript
exaQuark.push('update:state', {{EntityState}})
```



