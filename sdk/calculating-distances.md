# Calculating Distances



#### Get the distance between two entities

```
/**
* Returns the distance between two entities
* @param {string} [options.units] - the unit of measurement. Defaults to meters
*/
getDistanceBetweenEntities (entityOne, entityTwo, options)
```

#### Filter your list of neighbors by distance

```

/**
* Gets a list of neighbors within a specified distance
* @param {number} distance
* @param {string} [options.units] - the unit of measurement. Defaults to meters
* @param {string} [options.listType] - the list format to return. Defaults to Dictionary. Options: "Array" | "Dict"
*/
getNeighborsByMaxDistance (distance, options)
```



