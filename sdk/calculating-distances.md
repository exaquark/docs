# Helpers

`exaquark-js` comes with helpers for many of the more difficult functions. To use any of these you can import them:

```
import exaQuarkHelpers from 'exaquark-js/helpers'

// or you can import individual functions
import { getDistanceBetweenEntities } from 'exaquark-js/helpers'
```

# Calculating Distances

#### Get the distance between two entities

```
/**
* Returns the distance between two entities
* @param {string} [options.units] - the unit of measurement. Defaults to meters
*/
exaQuarkHelpers.getDistanceBetweenEntities (entityOne, entityTwo, options)
```

#### Filter your list of neighbors by distance

```
/**
* Gets a list of neighbors within a specified distance
* @param {number} distance
* @param {string} [options.units] - the unit of measurement. Defaults to meters
* @param {string} [options.listType] - the list format to return. Defaults to Dictionary. Options: "Array" | "Dict"
*/
exaQuarkHelpers.getNeighborsByMaxDistance (distance, options)
```



