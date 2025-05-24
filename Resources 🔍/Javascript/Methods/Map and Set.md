<iframe width="560" height="315" src="https://www.youtube.com/embed/hLgUTM3FOII" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
In JavaScript, **`Map`** and **`Set`** are two **new collections** introduced in **ECMAScript 6 (ES6)**, providing more advanced and efficient ways to work with key-value pairs and unique collections of values, respectively. Both `Map` and `Set` are objects but behave differently from traditional objects and arrays, offering specialized functionality.

### **Map**:

A **`Map`** is a collection of **key-value pairs**, where both the **keys** and **values** can be of any type (primitive or object). Unlike regular objects, the keys in a `Map` can be any type of value, including objects, functions, and even `undefined`. A `Map` remembers the **insertion order** of its elements, so the iteration order of the keys is consistent.

#### Key Features of `Map`:

1. **Any Type as Keys**:
    
    - In a `Map`, both the **keys** and **values** can be of any type. In regular JavaScript objects, keys are typically strings or symbols, but with `Map`, keys can be numbers, objects, arrays, and even other functions.
        
2. **Insertion Order**:
    
    - A `Map` maintains the **insertion order** of its elements. When you iterate over a `Map`, the items are returned in the order they were added.
        
3. **Built-in Methods**:
    
    - `set(key, value)`: Adds a new key-value pair or updates the value of an existing key.
        
    - `get(key)`: Retrieves the value associated with the specified key.
        
    - `has(key)`: Checks if the map contains a specific key.
        
    - `delete(key)`: Removes a key-value pair by the key.
        
    - `clear()`: Removes all key-value pairs from the map.
        
    - `size`: Returns the number of key-value pairs in the map.
        

#### Example of Using `Map`:

```javascript
const myMap = new Map();

// Adding key-value pairs
myMap.set('name', 'Alice');
myMap.set(1, 'one');
myMap.set(true, 'boolean');

// Accessing values
console.log(myMap.get('name'));  // 'Alice'
console.log(myMap.get(1));       // 'one'
console.log(myMap.get(true));    // 'boolean'

// Checking if a key exists
console.log(myMap.has('name'));  // true
console.log(myMap.has('age'));   // false

// Iterating over a Map
myMap.forEach((value, key) => {
  console.log(`${key}: ${value}`);
});

// Output:
// name: Alice
// 1: one
// true: boolean

// Deleting a key-value pair
myMap.delete(1);
console.log(myMap.has(1)); // false

// Size of the map
console.log(myMap.size); // 2
```

#### Iterating over a Map:

You can also use the `for...of` loop to iterate over `Map` entries, keys, or values.

```javascript
for (let [key, value] of myMap) {
  console.log(key, value);
}

// Iterating over keys
for (let key of myMap.keys()) {
  console.log(key);
}

// Iterating over values
for (let value of myMap.values()) {
  console.log(value);
}
```

### **Set**:

A **`Set`** is a collection of **unique values**. In a `Set`, each value can only appear once. If you try to add a duplicate value to a `Set`, it will be ignored. `Set` objects are useful when you need to store a collection of values with no duplicates, like unique items in an array.

#### Key Features of `Set`:

1. **Unique Values**:
    
    - A `Set` automatically removes duplicate values. If you add the same value multiple times, it will only appear once.
        
2. **Insertion Order**:
    
    - A `Set` also maintains the **insertion order** of its elements. When iterating over a `Set`, the order of elements is the same as the order in which they were added.
        
3. **Built-in Methods**:
    
    - `add(value)`: Adds a value to the set.
        
    - `has(value)`: Checks if a value is present in the set.
        
    - `delete(value)`: Removes a value from the set.
        
    - `clear()`: Removes all values from the set.
        
    - `size`: Returns the number of elements in the set.
        

#### Example of Using `Set`:

```javascript
const mySet = new Set();

// Adding values
mySet.add(1);
mySet.add(2);
mySet.add(3);
mySet.add(3);  // Duplicate, will be ignored
mySet.add('hello');
mySet.add({ name: 'Alice' });

// Checking if a value exists
console.log(mySet.has(1));     // true
console.log(mySet.has(4));     // false

// Iterating over a Set
mySet.forEach(value => {
  console.log(value);
});

// Output:
// 1
// 2
// 3
// hello
// { name: 'Alice' }

// Size of the set
console.log(mySet.size); // 5

// Deleting a value
mySet.delete(2);
console.log(mySet.has(2)); // false

// Clearing the set
mySet.clear();
console.log(mySet.size); // 0
```

#### Iterating over a Set:

You can use a `for...of` loop to iterate over the values of a `Set`.

```javascript
for (let value of mySet) {
  console.log(value);
}
```

### **Map vs Set**:

|**Feature**|**Map**|**Set**|
|---|---|---|
|**Purpose**|Stores key-value pairs|Stores unique values|
|**Key**|Maps can have any type as a key|Keys are not used; only values exist|
|**Duplicates**|Allows duplicate values for different keys|Only stores unique values, no duplicates|
|**Value Access**|Values are accessed by keys|Values are accessed directly|
|**Methods**|`set()`, `get()`, `has()`, `delete()`|`add()`, `has()`, `delete()`|

### **Use Cases for Map and Set**:

1. **Use `Map` when**:
    
    - You need to store key-value pairs where keys can be of any type (not just strings or symbols).
        
    - You need to maintain insertion order.
        
    - You need to frequently check for the existence of keys or retrieve values by key.
        
2. **Use `Set` when**:
    
    - You need to store a collection of unique values.
        
    - You want to eliminate duplicates from an array or list.
        
    - You need to maintain the insertion order of elements but don’t require keys.
        

### Conclusion:

- **`Map`** is ideal for storing key-value pairs with any type of key, and it provides methods for easy access, insertion, and deletion of keys and values.
    
- **`Set`** is useful for ensuring uniqueness of values and efficiently checking for the existence of a value.  
    Both `Map` and `Set` are part of modern JavaScript and provide efficient alternatives to traditional objects and arrays, especially when you need specialized behaviors like unique values or dynamic key-value storage.