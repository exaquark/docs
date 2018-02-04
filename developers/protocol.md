
# Protocol

A high level overview of the exaQuark protocol


##### Entity State


Any time you see `{{EntityState}}` in the documentation it is referring to [Entity State](entity-state.md), which is just a JS object with standard required data.

We have used `{{EntityState}}` to make the docs more readable.


{% method %}
## Authorise your connection

Request the entrypoint for the Metaverse.

{% sample lang="js" %}

```js
var allocatorUrl = 'https://enter.exaquark.net' // required
var apiKey = 'YOUR_API_KEY' // required
var universeId = 'TARGET_UNIVERSE_ID' // required
var transport = 'WEB_SOCKET' // required: WEB_SOCKET | UDP

var entryPoint = null // the url for the socket to connect to
var iid = null // the user's instance ID for this connection
requestEntrypoint (allocatorUrl, apiKey, universeId, transport) //@TODO, change this into native JS
.then(response => {
  entryPoint = response.entryPoint // URL for the universe which you can use to establish a socket connection
  iid = response.iid
})
```

{% sample lang="go" %}

```go
// @TODO
```

{% common %}
Sample response

```js
{
  "entryPoint": "999.999.999.999", // an IP address for the socket to connect to
  "iid": "ljsdf923-123kasd912-123-123" // your instance ID for this connection
}
```
{% endmethod %}



## Create a socket connection

Establish the connection with your location and state.

```javascript

// set up your initial state
var initialState = {{EntityState}}

// append your state to the endpoint
entryPoint += encodeURIComponent(initialState)
var socket = new WebSocket(url)
```

Once you have connected you will receive a stream of the following notifications:

## Notifications from exaQuark


###### exaQuark sends a full list of neighbors

Receive a full list of neighbours - your own IID will not be included in this list. Can be triggered from: socket connection/reconnection. exaQuark may send this sporadically to ensure consistency of neighborhood
When you receive this list, it is the latest and most up to date


```javascript
{
  method: 'neighbors'
  neighbors: [
    {{EntityState}},
    ...
  ]
}

```


##### Notification of changes in the neighborhood


```javascript
{
  method: 'updates'
  neighbors: [
    {{EntityState}},
    ...
  ]
}
```

##### Notifications about entities leaving the neighborhood

```javascript
{
  method: 'removes'
  neighbors: [
    // list of entities identified by the following
    {
      entityId: 234234, // their entityId
      iid: 29837928734, // instance ID
      dimension: 234234, // which dimension is the entitiy in
    }
  ]
}
```

##### Data is received

@TODO: explanation

```javascript
{
  method: 'data',
  source: {
    entityId: 234234,
    iid: 29837928734, // instance ID
    dimension: 1782687123, // which dimension this data came from
  },
  data: {

  }
}
```

## Messages to exaQuark

##### Update position and state

```javascript
socket.send(JSON.stringify({{EntityState}}))
```

##### Send data to all neighbors of a given level (delauney)

```javascript
socket.send(JSON.stringify({
  method:'data:broadcast',
  entityId: 234234,
  iid: 29837928734, // instance ID
  dimension: 234234, // source dimension
  reach: 1, // 1 - 5 delauney
  data: { }
}))
```

##### Send data to some neighbors

```javascript
socket.send(JSON.stringify({
  method:'data:private',
  entityId: 234234,
  iid: 29837928734, // instance ID
  dimension: 234234, // source dimension
  neigbours: [
    {
      entityId: 7687686,
      iid: 29837928734, // instance ID
    }
  ]
  data: { }
}))
```


##### Ask for a full list of neighbors

```javascript
socket.send(JSON.stringify({
  method:'ask:neighbors',
  entityId: 234234,
  iid: 29837928734, // instance ID
}))
```