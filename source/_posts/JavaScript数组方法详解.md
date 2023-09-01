---
title: JavaScript数组方法详解
categories: 1
tags: 前端
---
## 1.创建数组

### 1. 字面量创建数组

```js
var arr = []
```

### 2. 使用Array构造函数

> 创建一个空数组

```js
var arr = new Array()
```

> 如果只传一个数值参数，则表示创建一个初始长度为指定数值的空数组

```js
var arr = new Array(20)		// 创建一个包含20项的数组
```

> 如果传入一个非数值的参数或者参数个数大于 1，则表示创建一个包含指定元素的数组

```js
var arr3 = new Array("lily","lucy","Tom")		// 创建一个包含3个字符串的数组 
var array4 = new Array('23')		// ["23"]
```

### 3. Array.of 方法创建数组

> `Array.of()`方法总会创建一个包含所有传入参数的数组，而不管参数的数量与类型。

```js
let arr = Array.of(1, 2);
console.log(arr.length);//2

let arr1 = Array.of(3);
console.log(arr1.length);//1
console.log(arr1[0]);//3

let arr2 = Array.of('2');
console.log(arr2.length);//1
console.log(arr2[0]);//'2'
```

### 4.Array.from 方法创建数组

**`Array.from()`** 静态方法从[可迭代](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Iteration_protocols#可迭代协议)或[类数组](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#使用类数组对象)对象创建一个新的浅拷贝的数组实例。

> Map转数组

```js
let map = new Map([['a',1],['b',2]])

console.log(Array.from(map))		//[['a',1],['b',2]]
```

> Set转数组

```js
let set = new Set([1,2,3])

console.log(Array.from(set))		//[1,2,3]
```

> arguments转数组

```js
function foo() {
    console.log(Array.from(arguments))		//[1,2,3]
}
foo(1,2,3)
```

> 类对象转数组

```js
let obj = {
    0: 1,
    1: 2,
    2: 3,
    length: 3
}
console.log(Array.from(obj))		//[1,2,3]
```

### 5. Array.from的映射转换

> Array.from方法接受第二个参数

```js
let obj = {
    0: 1,
    1: 2,
    2: 3,
    length: 3
}
Array.from(obj,(item,index)=>{
    console.log(item,index)
    return item
})
//1 0
//2 1
//3 2
```

> 如果映射函数需要在对象上工作，你可以手动传递第三个参数给 Array.from()方法，从而指定映射函数内部的 this 值

```js
const helper = {
  diff: 1,
  add(value) {
    return value + this.diff;
  }
}

function translate() {
 //arguments 是一个对应于传递给函数的参数的类数组对象
  return Array.from(arguments, helper.add, helper); 
}

let arr = translate('liu', 26, 'man');
console.log(arr); // ["liu1", 27, "man1"]
```

## 2. 数组原型链上的方法

- `join()`：用指定的分隔符将数组每一项拼接为字符串

- `push()` ：向数组的末尾添加新元素

- `pop()`：删除数组的最后一项

- `unshift()`：向数组首位添加新元素
- `shift()`：删除数组的第一项

- `slice()`：按照条件查找出其中的部分元素

- `splice()`：对数组进行增删改

- `fill()`: 方法能使用特定值填充数组中的一个或多个元素

- `filter()`:“过滤”功能

- `concat()`：用于连接两个或多个数组

- `indexOf()`：检测当前值在数组中第一次出现的位置索引

- `lastIndexOf()`：检测当前值在数组中最后一次出现的位置索引

- `every()`：判断数组中每一项都是否满足条件

- `some()`：判断数组中是否存在满足条件的项

- `includes()`：判断一个数组是否包含一个指定的值

- `sort()`：对数组的元素进行排序

- `reverse()`：对数组进行倒序

- `forEach()`：ES5 及以下循环遍历数组每一项

- `map()`：ES6 循环遍历数组每一项

- `copyWithin()`:用于从数组的指定位置拷贝元素到数组的另一个指定位置中

- `find()`:返回匹配的值

- `findIndex()`:返回匹配位置的索引

- `toLocaleString()、toString()`:将数组转换为字符串

- `flat()、flatMap()`：扁平化数组

- `entries() 、keys() 、values()`:遍历数组

### 1. join()

> **`join()`** 方法将一个数组（或一个[类数组对象](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Indexed_collections#使用类数组对象)）的所有元素连接成一个字符串并返回这个字符串，用逗号或指定的分隔符字符串分隔。如果数组只有一个元素，那么将返回该元素而不使用分隔符

```js
const arr = ['Fire', 'Air', 'Water'];

console.log(arr.join());
// Expected output: "Fire,Air,Water"

console.log(arr.join(''));
// Expected output: "FireAirWater"

console.log(arr.join('-'));
// Expected output: "Fire-Air-Water"
```

### 2. push()

> **`push()`** 方法将指定的元素添加到数组的末尾，并返回新的数组长度。

```js
let arr = ['a','b']
console.log(arr.push('c'))		//3
console.log(arr)		//['a','b','c']
```

### 3. pop()

> **`pop()`** 方法从数组中删除**最后一个**元素，并返回该元素的值。此方法会更改数组的长度。

```js
let arr = ['a','b','c']
console.log(arr.pop())		//c
console.log(arr)		['a','b']
```

### 4. unshift()

> **`shift()`** 方法将指定元素添加到数组的开头，并返回数组的新长度。

```js
let arr = ['a','b']
console.log(arr.push('c'))		//3
console.log(arr)		//['c','a','b']
```

### 5. shift()

> **`shift()`** 方法从数组中删除**第一个**元素，并返回该元素的值。此方法更改数组的长度。

```js
let arr = ['a','b','c']
console.log(arr.pop())		//a
console.log(arr)		['b','c']
```

### 6. sort()

> **`sort()`** 方法[*就地*](https://zh.wikipedia.org/wiki/原地算法)对数组的元素进行排序，并返回对相同数组的引用。默认排序是将元素转换为字符串，然后按照它们的 UTF-16 码元值升序排序。
>
> 由于它取决于具体实现，因此无法保证排序的时间和空间复杂度。
>
> 如果想要不改变原数组的排序方法，可以使用 [`toSorted()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/toSorted)。

```js
const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// Expected output: Array ["Dec", "Feb", "Jan", "March"]

const array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1);
// Expected output: Array [1, 100000, 21, 30, 4]
```

> **`sort()`**接受一个函数类型的参数`compareFn`，用于排序
>
> `compareFn`函数接受两个参数
>
> `a`：第一个用于比较的元素。不会是 `undefined`
>
> `b`：第二个用于比较的元素。不会是 `undefined`

```js
let arr = [4,2,6,3,5,1]
arr.sort((a,b)=>a-b)
// Expected output: Array [ 1, 2, 3, 4, 5, 6 ]
arr.sort((a,b)=>b-a)
// Expected output: Array [ 6, 5, 4, 3, 2, 1 ]
```

| `compareFn(a, b)` 返回值 | 排序顺序                   |
| :----------------------- | :------------------------- |
| > 0                      | `a` 在 `b` 后，如 `[b, a]` |
| < 0                      | `a` 在 `b` 前，如 `[a, b]` |
| === 0                    | 保持 `a` 和 `b` 原来的顺序 |

### 7. reverse()

> reverse() 方法用于颠倒数组中元素的顺序。

```js
var arr = [13, 24, 51, 3];
console.log(arr.reverse());   //[3, 51, 24, 13]
console.log(arr);   //[3, 51, 24, 13](原数组改变)
```

### 8. concat()

> **`concat()`** 方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。

```js
let arr = [1,3,5,7];
let arrCopy = arr.concat(9,[11,13],[14,15]);
console.log(arrCopy);   //[1, 3, 5, 7, 9, 11, 13,14,15]
console.log(arr);   // [1, 3, 5, 7](原数组未被修改)
```

> slice()：返回从原数组中指定开始下标到结束下标之间的项组成的新数组
>
> slice()方法可以接受一或两个参数，即要返回项的起始和结束位置
>
> 在**只有一个参数**的情况下， slice()方法返回从该参数指定位置开始到当前数组末尾的所有项
>
> 如果**有两个参数**，该方法返回起始和结束位置之间的项，但不包括结束位置的项

### 9.splice()

> **`splice()`** 方法通过移除或者替换已存在的元素和/或添加新元素[就地](https://zh.wikipedia.org/wiki/原地算法)改变一个数组的内容。
