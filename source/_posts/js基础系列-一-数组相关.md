---
title: 'js基础系列(一):数组相关'
date: 2019-09-08 23:50:19
tags:
---

#常用数组方法

## 1-1 Array.map()

> 此方法是将数组中的每个元素调用一个提供的函数，结果作为一个新的数组返回，并没有改变原来的数组

```
let arr = [1, 2, 3, 4, 5]
let newArr = arr.map(x => x*2)
console.log(arr);       //arr= [1, 2, 3, 4, 5]   原数组保持不变
console.log(newArr);    //newArr = [2, 4, 6, 8, 10] 返回新数组
   
```

## 1-2 Array.forEach()

> 此方法是将数组中的每个元素执行传进提供的函数，没有返回值，直接改变原数组，注意和map方法区分

```
let arr = [1, 2, 3, 4, 5]
num.forEach(x => x*2)
   // arr = [2, 4, 6, 8, 10]  数组改变,注意和map区分
```

## 1-3 Array.filter()

> 此方法是将所有元素进行判断，将满足条件的元素作为一个新的数组返回

```
let arr = [1, 2, 3, 4, 5]
let isBigEnough => value => value >= 3
let newArr = arr.filter(isBigEnough )
    //newNum = [3, 4, 5] 满足条件的元素返回为一个新的数组
```

## 1-4 Array.push(new)

> 此方法是在数组的后面添加新加元素，此方法改变了数组的长度

```
let arr = [1,2]
arr.push(3)
console.log(arr) //[1,2,3x]
```



## 1-5 Array.pop()

> 此方法在数组后面删除最后一个元素，并返回数组，此方法改变了数组的长度：

```
let arr = [1, 2, 3, 4, 5]
    arr.pop()
    console.log(arr) //[1, 2, 3, 4]
    console.log(arr.length) //4
```



## 1-6 Array.shift()

> 此方法在数组后面删除第一个元素，并返回数组，此方法改变了数组的长度

```
let arr = [1, 2, 3, 4, 5]
    arr.shift()
    console.log(arr) //[2, 3, 4, 5]
    console.log(arr.length) //4 
```



## 1-7 Array.unshift()

> 此方法是将一个或多个元素添加到数组的开头，并返回新数组的长度

```
let arr = [1, 2, 3, 4, 5]
    arr.unshift(6, 7)
    console.log(arr) //[6, 7, 2, 3, 4, 5]
    console.log(arr.length) //7 
```

## 1-8 Array.isArray()

> 判断一个对象是不是数组，返回的是布尔值

```
let arr = [1,2]
Array.isArray(arr) // true
```

## 1-9 Array.concat()

> 此方法是一个可以将多个数组拼接成一个数组

```
let arr1 = [1, 2, 3],
    arr2 = [4, 5]
  let arr = arr1.concat(arr2)
  console.log(arr)//[1, 2, 3, 4, 5]
```

## 1-10 Array.toString()

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

## 1-11 Array.join()

> 此方法也是将数组转化为字符串

```
let arr = [1, 2, 3, 4, 5];
arr.join('-') //1-2-3-4-5
```

## 1-12 Array.splice(开始位置， 删除的个数，元素)

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



## 1-13 reduce()

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



### 7-13-1 数组求和

```
let arr = [1,2,3,1,2]
getSum = (all,now) => {
    return  all + now
}
let sum = arr.reduce(getSum)
console.log(`sum=${sum}`);  // sum=9

```

### 1-13-2 数组求最大值

```
let arr = [1,2,3,1,2]
getMax = (a,b) => {
    return Math.max(a,b)
}
let max = arr.reduce(getMax)
console.log(`max=${max}`); // max=3
```

### 1-13-3 数组去重

```
let arr = [1,2,3,1,2]
getOnlyOne = (total,cur) => {
    total.indexOf(cur) === -1 && total.push(cur)
    return total
}
let newArr = arr.reduce(getOnlyOne,[])
console.log(newArr); // [1,2,3]
```



#二.数组去重

数组中包含对象的时候需要做去重处理的方法

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



