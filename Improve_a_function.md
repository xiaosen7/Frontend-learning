Hi all, I'm going to share a frontend coding question for you. That is to improve a function posted by https://bigfrontend.dev/problem/improve-a-function.

We are given such code, and we are asked some questions.

// Given an input of array, 
// which is made of items with >= 3 properties
```js
let items = [
  {color: 'red', type: 'tv', age: 18}, 
  {color: 'silver', type: 'phone', age: 20},
  {color: 'blue', type: 'book', age: 17}
] 

// an exclude array made of key value pair
const excludes = [ 
  {k: 'color', v: 'silver'}, 
  {k: 'type', v: 'tv'}, 
  ...
] 

function excludeItems(items, excludes) { 
  excludes.forEach( pair => { 
    items = items.filter(item => item[pair.k] === item[pair.v])
  })

  return items
} 
```
1. What does this function excludeItems do?
The function named excludeItems receives two parameters: items array and exludes array. The items array is an object array which is made of more than 3 properties. While he excludes array is also an object array but the properties are constantly inlcudes: k, v. Obviously, the function will use excludes array to filter out items by k and v where if the item has the property key same with the k property of some items of excludes and the corresponding property value euqals the value of property v of item.

2. Is this function working as expected ?
No, there are two errors in the function body, one is the three-equal signs, it should be not-equal signs. Another is the value of `item[pari.v]`, it should be `pair.v`.

3. What is the time complexity of this function?
If we assume the length of items array is n, and the length of exludes array is m, then the time complexity is o(m*n), because there are two nested loops(forEach and filter), and each loop is entire loop.

4. How would you optimize it ?
My optimized code is as follows:

```js
function excludeItems(items, excludes) {
  const map = new Map();
  for (const { k, v } of excludes) {
    if (!map.has(k)) {
      map.set(k, new Set());
    }

    map.get(k).add(v);
  }

  return items.filter((item) => Object.keys(item).every(key => !map.has(key) || !map.get(key).has(item[key])))
}

```
Firstly, there is a map which the key is k property value in exludes array, and the value is a set which contains all the values which are from the same k property in excludes array. I use a for of loop statement to iterate over each item of exlude array to build this map.
Secondly, I use filter method to filter out items array and use every method posted by es6 to check the keys of item whether all keys are either not existed in map or their corresponding values are not in the set. 
