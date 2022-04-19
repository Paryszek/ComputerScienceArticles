# JavaScript - difference between slice and splice methods

JavaScript has in its arsenal very similar array methods “slice” and “splice”. Ability to differentiate between this two methods can be really handy. Each one can be used in different scenarios, and can be really helpful someday during your programming sessions.

 Did you ever meet with this methods during interview? In todays post I will explain them together with examples.

Both of this methods manipulates elements inside existing array structure.

# S**lice**

```jsx
slice();
slice(start);
slice(start, end);
```

Method takes full or just part of the array and returns it as a new array. Start index and end index parameters are used to mark the section of the array, without passing any parameters the full array is marked as default. The elements from marked section will be returned as new array copy, without changing original array. 

## Example

```jsx
var animals = ['dog', 'cat', 'monkey', 'donkey', 'dino', 'elephant'];

animals.slice();
// output: ["dog", "cat", "monkey", "donkey", "dino", "elephant"]

animals.slice(0);
// output: ["dog", "cat", "monkey", "donkey", "dino", "elephant"]

animals.slice(1);
// output: ["cat", "monkey", "donkey", "dino", "elephant"]

animals.slice(0, 1)
// output: ["dog"]

animals.slice(0, 2)
// output: ["dog", "cat"]

animals.slice(2, 2)
// output: []

animals.slice(2, 3)
// output: ["monkey"]

animals.slice(2, 5)
// output: ["monkey", "donkey", "dino"]
```

# Splice

```jsx
splice(start)
splice(start, deleteCount)
splice(start, deleteCount, args...)
```

Method have start index parameter and two optional parameters deleteCount and elements. Start index parameter marks start of the section. DeleteCount parameter marks how much elements will be replaced/deleted. Passed elements will be added in section determined by two previous parameters. When there is no elements, method just removes section of array and returns it as new array. If deleteCount parameter is equal 0, the method won’t delete anything, it can be used to adding new passed elements. To replace / remove existing elements with passed elements, deleteCount parameter should be equal or bigger than start index parameter. 

Splice method in contrary to slice method changes the array state. Method itself is very powerful but can be hard to understand at first sight. Hopefully below example should explain how to use this method.

## Example

```jsx
var fruits = ["Banana", "Orange", "Apple", "Mango"];

fruits.splice(2, 0, "Lemon", "Kiwi");
// fruits array: Banana, Orange, Lemon, Kiwi, Apple, Mango result: empty

fruits.splice(0, 2, "Lemon", "Kiwi");
// fruits array: [Lemon, Kiwi, Apple, Mango] result: [Banana, Orange]
```

# Summary

Slice is fast-forward method unlike Splice which can be more catchy to get you head around it. They are easy to confuse with each other, as my interviewer experience showed me, because of name similarity. Its in your best front-end developer intrest to understand them. 

As you can see there are few differences between this two methods and I hope my article helped you understand them a little. I recommend you to use this methods to create some simple examples for better understanding. Knowing this functions is really crucial because they can be useful for some typical programming solutions.
