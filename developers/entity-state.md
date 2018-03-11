# Entity State

The following is a representation of an entity in a universe. It is the standard format that is sent and received from exaQuark.

Any time you see `{{EntityState}}` in the documentation it is referring to the following format.

```js
{
  entityId: 'MOCK_ENTITY_ID', // {string} required: their entityId
  iid: 'MOCK_IID', // {string} required: instance ID - each user can have multiple "instances". For example they can be logged in to their browser and their phone at the same time
  universe: 'MOCK_UNIVERSE_ID', // {string} optional:  which universe is the entity in. Default: Sandbox
  neighborLevel: 1, // {number} 1 - 5 - the "relative distance" of your neighbor. It isn't required when sending to exaQuark, however you will receive it in notifications about your neighbors
  geo: {
    lat: 3.11, // {double} required: latitude
    lng: 5.33, // {double} required: longitude
    altitude: 32.1, // {double} optional: altitude in meters - can be negative
    rotation: [ 2, 5, 19 ] // {Array of doubles} optional: all in degrees. Default facing north
  },
  properties: {
    displayName: 'A_USER_NAME', // {string} required: a human readable name to be displayed
    sound: true, // {boolean} optional: defaults to true. false === mute
    mic: true, // {boolean} optional: defaults to true. false === muted microphone
    virtualPosition: false, // {boolean} optional: defaults to false. Is this person physically in the position that they are in the digital universe. (true === they are not physically present there)
    entityType: 'HUMAN' // {string} optional: defaults to 'HUMAN'. Options: 'HUMAN' | 'BOT' | 'DRONE'
  },
  customState: {
    // developer defined state for their universe
    // you can use this to pass arbitrary data to other entities in your neighborhood
  }
}
```



