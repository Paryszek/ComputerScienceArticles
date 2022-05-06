# JavaScript - simple explanation of shift, unshift, push, pop methods

In JavaScript language is available Array as global object. As we all know Array is a structure that can help us store large number of elements, but how to manage this series of elements? 

Today I would like to present you simple reminder of useful methods, that we can all use for handling I/O operations on Arrays. This methods can be used on single elements only.

## Push

Is **inserting** element at the **end of array** and returns new length of the array as the result.

```jsx
const array = [1, 2];

var result = array.push(3);

console.log(array); // [1, 2, 3];
console.log(result); // new array length 3
```

## Pop

Is **removing** the **last element** from the array and returns this element as the result.

```jsx
const array = [1, 2];

const result = array.pop();

console.log(array); // [1];
console.log(result); // number 2
```

## Unshift

Is **inserting** element at the **beginning of array** and returns new length of the array as the result.

```jsx
const array = [1, 2];

const result = array.unshift(3);

console.log(array); // [3, 1 ,2];
console.log(result); // new array length 3
```

## Shift

Is **removing** the **first element** of the array and returns it as a result.

```jsx
const array = [1, 2];

const result = array.shift();

console.log(array); // [2];
console.log(result); // number 1
```

## Summary

Short and simple explanation is a good path to remember it for a longer time. **Push** and **Pop** methods are clearly more common, as they are used for the end of the array. **Unshift** and **Shift** methods are used rather rarely, and are intended for the beginning of the array. 

This Array functions are good foundations for programming data structures like **Heap** or **Binary Tree.**

I Hope this short article will help you understand how this methods work, and help you remember it for the future or if you already knew tis functions, short refreshment of your knowledge is also good achievement.
