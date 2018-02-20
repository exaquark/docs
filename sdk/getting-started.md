# JS SDK

## Installation

```
npm install exaquark-js --save
```

##### Entity State

Any time you see `{{EntityState}}` in the documentation it is referring to [Entity State](/developers/entity-state.html), which is just a JS object with standard required data.

We have used `{{EntityState}}` to make the docs more readable.

## Usage

##### Set up

```javascript
const exaQuarkJs = require('exaquark-js/core')
const exaQuarkUrl = 'https://enter.exaquark.com'
var apiKey = 'YOUR_API_KEY' // {String} required
let options = {
  entityId: 'ENTITY_ID', // {String} required
  universe: 'UNIVERSE_ID', // {String} optional: defaults to sandbox
  transport: 'WebSocket', // {String} optional: WebSocket | UDP
  logger: (msg, data) => { console.log(msg, data) }, // optional: attach your own logger
}
var iid = null // exaQuark will generate - A user can have multiple instance ID's (eg, one for their phone, one for their AR glasses)
var exaQuark = new exaQuarkJs(exaQuarkUrl, apiKey, options)

// Subscribe to the individual neighborhood events - see "Notifications from exaQuark" below
exaQuark.on("neighbor:enter", {{EntityState}} => {
  create({{EntityState}}) // example function in your app
})
exaQuark.on("neighbor:leave", {{EntityState}} => {
  remove({{EntityState}}) // example function in your app
})
exaQuark.on("neighbor:updates", {{EntityState}} => {
  update({{EntityState}}) // example function in your app
})
exaQuark.on("data", data => {
  handleData(data) // example function in your app
})
```

##### Connect to a universe

```javascript
// Connect to the universe!
let initialState = {{EntityState}} // your user's position and state
exaQuark.connect(initialState).then(({ myIid }) => {
  iid = myIid 
}).catch('err', err => { console.error(err) })
```

**At any time you can get an up-to-date array of your neighbors**

```javascript
// Returns an Array of {{EntityState}}s
let neighbors = exaQuark.neighbors()
```



