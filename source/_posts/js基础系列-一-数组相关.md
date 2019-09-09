---
title: 'js基础系列(一):数组相关'
date: 2019-09-08 23:50:19
tags:js基础系列
---

#一,常用数组方法



## 1-1 arr.map()

> 此方法是将数组中的每个元素调用一个提供的函数，结果作为一个新的数组返回，并没有改变原来的数组

```
let arr = [1, 2, 3, 4, 5]
let newArr = arr.map(x => x*2)
console.log(arr);       //arr= [1, 2, 3, 4, 5]   原数组保持不变
console.log(newArr);    //newArr = [2, 4, 6, 8, 10] 返回新数组
   
```

## 1-2 arr.forEach()

> 此方法是将数组中的每个元素执行传进提供的函数，没有返回值，直接改变原数组，注意和map方法区分

```
let arr = [1, 2, 3, 4, 5]
num.forEach(x => x*2)
   // arr = [2, 4, 6, 8, 10]  数组改变,注意和map区分
```

## 1-3 arr.filter()

> 此方法是将所有元素进行判断，将满足条件的元素作为一个新的数组返回

```
let arr = [1, 2, 3, 4, 5]
let isBigEnough => value => value >= 3
let newArr = arr.filter(isBigEnough )
    //newNum = [3, 4, 5] 满足条件的元素返回为一个新的数组
```

## 1-4 arr.push(new)

> 此方法是在数组的后面添加新加元素，此方法改变了数组的长度

```
let arr = [1,2]
arr.push(3)
console.log(arr) //[1,2,3x]
```



## 1-5 arr.pop()

> 此方法在数组后面删除最后一个元素，并返回数组，此方法改变了数组的长度：

```
let arr = [1, 2, 3, 4, 5]
    arr.pop()
    console.log(arr) //[1, 2, 3, 4]
    console.log(arr.length) //4
```



## 1-6 arr.shift()

> 此方法在数组后面删除第一个元素，并返回数组，此方法改变了数组的长度

```
let arr = [1, 2, 3, 4, 5]
    arr.shift()
    console.log(arr) //[2, 3, 4, 5]
    console.log(arr.length) //4 
```



## 1-7 arr.unshift()

> 此方法是将一个或多个元素添加到数组的开头，并返回新数组的长度

```
let arr = [1, 2, 3, 4, 5]
    arr.unshift(6, 7)
    console.log(arr) //[6, 7, 2, 3, 4, 5]
    console.log(arr.length) //7 
```

## 1-8 arr.isArray()

> 判断一个对象是不是数组，返回的是布尔值

```
let arr = [1,2]
Array.isArray(arr) // true
```

## 1-9 arr.concat()

> 此方法是一个可以将多个数组拼接成一个数组

```
let arr1 = [1, 2, 3],
    arr2 = [4, 5]
  let arr = arr1.concat(arr2)
  console.log(arr)//[1, 2, 3, 4, 5]
```

## 1-10 arr.toString()

> 此方法将数组转化为字符串

```
let arr = [1, 2, 3, 4, 5];
let str = arr.toString()
   console.log(str)// 1,2,3,4,5

let str1 = arr.toString()
let str2 = arr.toString(',')
let str3 = arr.toString('##')
   console.log(str1)// 12345
   console.log(str2)// 1,2,3,4,5
   console.log(str3)// 1##2##3##4##5
```

## 1-11 arr.join()

> 此方法也是将数组转化为字符串

```
let arr = [1, 2, 3, 4, 5];
arr.join('-') //1-2-3-4-5
```

## 1-12 arr.splice(开始位置， 删除的个数，元素)

> 　万能方法，可以实现增删改，然后返回被删除的项目。。注意：该方法会改变原始数组

```
//1.新增元素
let a = [1, 2, 3, 4, 5];
let a1 =  a.splice(2, 0, 'haha')
console.log(a) //[1, 2, 'haha', 3, 4, 5]新增一个元素
console.log(a1) //[]  返回被删除的项目

// 2.删除元素
let b = [1, 2, 3, 4, 5];
let b1 =  b.splice(2, 3)
console.log(b); // [1,2]
console.log(b1) //[3, 4, 5]

// 3.替换元素
let c = [1, 2, 3, 4, 5];
let c1 =  c.splice(2, 1,'haha')
console.log(c); // [ 1, 2, 'haha', 4, 5 ]
console.log(c1) //[3]
```



## 1-13 arr.slice()

> splice() 方法可删除从 index 处开始的零个或多个元素，并且用参数列表中声明的一个或多个值来替换那些被删除的元素。如果从 arrayObject 中删除了元素，则返回的是含有被删除的元素的数组。splice() 方法会直接对数组进行修改。

~~~
let arr = [1,2,3,4,5,6]
let newArr = arr.slice(1,2)
console.log(newArr); //[ 2 ]
console.log(arr); //[ 1, 2, 3, 4, 5, 6 ]
~~~



##1-14  arr.sort()

> 按照 Unicode code 位置排序，默认升序

~~~
let arr = [21,12,3,4,5,6]

arr.sort()
console.log(arr); //[21,12,3,4,5,6]
~~~

- 升序

~~~
let arr = [21,12,3,44,5,6]

arr.sort((a,b)=>{
    return a-b
})
console.log(arr); //[ 3, 5, 6, 12, 21, 44 ]
~~~

- 降序

~~~
let arr = [21,12,3,44,5,6]

arr.sort((a,b)=>{
    return b-a
})
console.log(arr); //[ 44, 21, 12, 6, 5, 3 ]
~~~



##1-15 arr.reverse()

> reverse() 方法用于颠倒数组中元素的顺序。返回的是颠倒后的数组，会改变原数组。

~~~
let arr = [21,12,3,44,5,6]

arr.reverse()
console.log(arr); //[ 6, 5, 44, 3, 12, 21 ]
~~~



## 1-16 indexOf 和 lastIndexOf

> 都是查找数组元素 出现的位置。都接受两个参数：查找的值、查找起始位置
> 不存在，返回 -1 ；存在，返回位置。
>
> indexOf 是从前往后查找， lastIndexOf 是从后往前查找。

~~~
let arr = [21,12,3,44,5,6]
console.log(arr.indexOf(12)); //1
~~~

# 二,es6新增的数组操作



## 2-1 reduce()

语法

```
arr.reduce(function(prev,cur,index,arr){
...
}, init);
```

**arr** 表示原数组；
**prev** 表示上一次调用回调时的返回值，或者初始值 init;
**cur** 表示当前正在处理的数组元素；
**index** 表示当前正在处理的数组元素的索引，若提供 init 值，则索引为0，否则索引为1；
**init** 表示初始值。



### 2-1-1 数组求和

```
let arr = [1,2,3,1,2]
getSum = (all,now) => {
    return  all + now
}
let sum = arr.reduce(getSum)
console.log(`sum=${sum}`);  // sum=9

```

### 2-1-2 数组求最大值

```
let arr = [1,2,3,1,2]
getMax = (a,b) => {
    return Math.max(a,b)
}
let max = arr.reduce(getMax)
console.log(`max=${max}`); // max=3
```

### 2-1-3 数组去重

```
let arr = [1,2,3,1,2]
getOnlyOne = (total,cur) => {
    total.indexOf(cur) === -1 && total.push(cur)
    return total
}
let newArr = arr.reduce(getOnlyOne,[])
console.log(newArr); // [1,2,3]
```



##2-2 arr.every()

> 定义和用法

every() 方法用于检测数组所有元素是否都符合指定条件（通过函数提供）。

every() 方法使用指定函数检测数组中的所有元素：

- 如果数组中检测到有一个元素不满足，则整个表达式返回 *false* ，且剩余的元素不会再进行检测。
- **如果所有元素都满足条件，则返回 true**。

**注意：** every() 不会对空数组进行检测。

**注意：** every() 不会改变原始数组。

- 语法

```
语法：array.every(function(item,index,array）{
               //item:当前元素的值；

                    //index:当前元素的索引；

                    // array:当前元素的数组对象；

                })
```

- 用法

```
let a = [1,2,3,4].every((item)=>{return item > 5})
console.log(a) // false

let b = [1,2,3,4].every((item)=>{return item > 2})
console.log(b) // false

let c = [1,2,3,4].every((item)=>{return item >= 1})
console.log(c) // true
```



## 2-13 arr.some()

> 定义和用法

some() 方法用于检测数组中的元素是否满足指定条件（函数提供）。

some() 方法会依次执行数组的每个元素：

- **如果有一个元素满足条件，则表达式返回*true*** , 剩余的元素不会再执行检测。
- 如果没有满足条件的元素，则返回false。

**注意：** some() 不会对空数组进行检测。

**注意：** some() 不会改变原始数组。

- 语法

```
语法：array.some(function(item,index,array){
                    //item:当前元素的值；

                    //index:当前元素的索引；

                    // array:当前元素的数组对象；

                })
```

- 用法

```
let a = [1,2,3,4].some((item)=>{return item>5})
console.log(a) // false

let b = [1,2,3,4].some((item)=>{return item<2})
console.log(b) // true

let c = [1,2,3,4].some((item)=>{return item<1})
console.log(c) // false
```



##2-4 arr.filfter()

> 定义和用法

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素。

**注意：** filter() 不会对空数组进行检测。

**注意：** filter() 不会改变原始数组。

~~~
let arr = [21,12,3,44,5,6]
let a = arr.filter((item)=>{
    return item > 10
})
console.log(a); //[ 21, 12, 44 ]
console.log(arr); //[ 21, 12, 3, 44, 5, 6 ]
~~~



## 2-5 arr.map()

> 定义和用法

map() 方法返回一个新数组，数组中的元素为原始数组元素调用函数处理后的值。

map() 方法按照原始数组元素顺序依次处理元素。

**注意：** map() 不会对空数组进行检测。

**注意：** map() 不会改变原始数组。返回每次函数调用的结果组成一个新数组

> 语法

~~~
array.map(function(currentValue,index,arr), thisValue)
~~~

- currentValue   必须。当前元素的值
- index                可选。当前元素的索引值
- arr                    可选。当前元素属于的数组对象

> 用法

~~~
let arr = [21,12,3,44,5,6]
let a = arr.map((item)=>{
    return item > 10
})
console.log(a); //[ true, true, false, true, false, false ]
console.log(arr); //[ 21, 12, 3, 44, 5, 6 ]
~~~



## 2-6 arr.find()

> 定义和用法

find() 方法返回通过测试（函数内判断）的数组的第一个元素的值。

find() 方法为数组中的每个元素都调用一次函数执行：

- 当数组中的元素在测试条件时返回 *true* 时, find() 返回符合条件的元素，之后的值不会再调用执行函数。
- 如果没有符合条件的元素返回 undefined

**注意:** find() 对于空数组，函数是不会执行的。

**注意:** find() 并没有改变数组的原始值。

> 语法

```
array.find(function(currentValue, index, arr),thisValue)
```

- currentValue   必须。当前元素的值
- index                可选。当前元素的索引值
- arr                    可选。当前元素属于的数组对象

> 用法
>

~~~
let arr = [4,22,3,44,5,6]
let a = arr.find((item)=>{
    return item > 10
})
console.log(a); //2
console.log(arr); //[ 4, 22, 3, 44, 5, 6 ]
~~~



## 2-7 arr.findIndex()

> 定义和用法

findIndex() 方法返回传入一个测试条件（函数）符合条件的数组第一个元素位置。

findIndex() 方法为数组中的每个元素都调用一次函数执行：

- 当数组中的元素在测试条件时返回 *true* 时, findIndex() 返回符合条件的元素的索引位置，之后的值不会再调用执行函数。
- 如果没有符合条件的元素返回 -1

**注意:** findIndex() 对于空数组，函数是不会执行的。

**注意:** findIndex() 并没有改变数组的原始值。

> 语法

~~~
array.findIndex(function(currentValue, index, arr), thisValue)
~~~

> 用法

~~~
let arr = [4,22,3,44,5,6]
let a = arr.findIndex((item)=>{
    return item > 10
})
console.log(a); //1
console.log(arr); //[ 4, 22, 3, 44, 5, 6 ]
~~~



## 2-8 arr.entries()

entries() 方法返回一个数组的迭代对象，该对象包含数组的键值对 (key/value)。

迭代对象中数组的索引值作为 key， 数组元素作为 value。

~~~
let arr = ["Banana", "Orange", "Apple", "Mango"];
for(let item of arr.entries()){
    console.log(item); 
}

/*
[ 0, 'Banana' ]
[ 1, 'Orange' ]
[ 2, 'Apple' ]
[ 3, 'Mango' ]
 */
~~~



## 2-9 arr.values()

返回迭代器：返回键值对的value。（对比参考arr.entries()）

```
let arr = ["Banana", "Orange", "Apple", "Mango"];
for(let item of arr.values()){
    console.log(item); 
}

/**
 Banana
Orange
Apple
Mango
 */
```



## 2-10 arr.keys()

keys() 方法用于从数组创建一个包含数组键的可迭代对象。

如果对象是数组返回 true，否则返回 false。

~~~
let arr = ["Banana", "Orange", "Apple", "Mango"];
for(let item of arr.keys()){
    console.log(item); 
}

/**
0
1
2
3
 */
~~~









#三.数组去重

主要介绍数组中包含对象的时候需要做去重处理的方法

### 1-1.reduce

~~~
var arr = [
    { name: "张三", num: "1" },
    { name: "李四", num: "11" },
    { name: "王五", num: "12" },
    { name: "张三", num: "13" },
    { name: "李四", num: "1" },
    { name: "王五", num: "12" }
  ]
 
  /**
   * 
   * @param {*} arr 需要去重的原数组 
   * @param {*} name  去重字段
   * @return  去重之后的新数组
   */
 function arrayUnique2(arr, name) {
    var hash = {};
    return arr.reduce(function (item, next) {
      hash[next[name]] ? '' : hash[next[name]] = true && item.push(next);
      return item;
    }, []);
  }
  
 arrayUnique2(arr, "name"); 
 
 /** [ { name: '张三', num: '1' },
  { name: '李四', num: '11' },
  { name: '王五', num: '12' } ]  **/
~~~



### 1-2 for循环

借助对象访问属性的方法，判断属性是否存在，如果已存在则进行过滤

~~~
var arr = [
    { name: "张三", num: "1" },
    { name: "李四", num: "11" },
    { name: "王五", num: "12" },
    { name: "张三", num: "13" },
    { name: "李四", num: "1" },
    { name: "王五", num: "12" }
  ]
  
 function deleteSameItemInArray (targetArr,itemName=''){
    let obj = {},result=[]
    targetArr.forEach((item,i)=>{
        if(!obj[item[itemName]]){
            obj[item[itemName]] = true
            result.push(item)
        }
    })
    return result
  }

 let resultArr = deleteSameItemInArray(arr2,'name')
console.log(resultArr);
~~~



