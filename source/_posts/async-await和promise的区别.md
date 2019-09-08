---
title: async-await和promise的区别
date: 2019-08-12 16:23:51
tags:
---

为什么要写这篇文章？在面试的时候被问过这个问题，虽然在工作中这两种都用过，但是确实是没考虑过有什么区别，今天再重学一遍。



## 1  promise

Promise,简单来说就是一个容器，里面保存着某个未来才会结束的时间，从语法上来说，Promise是一个对象，从它可以获取异步操作的消息。

基本语法：

```
var p1 = new Promise(test);
var p2 = p1.then(function (result) {
    console.log('成功：' + result);
});
var p3 = p2.catch(function (reason) {
    console.log('失败：' + reason);
});


//支持链式操作
p1.then(function (result) {
    console.log('成功：' + result);
}).catch(function (reason) {
    console.log('失败：' + reason);
});

```

## 2 promsie有三种状态

ending、fulfilled、rejected(未决定，履行，拒绝)。同一时间只能存在一种状态，且状态一旦改变就不能在变

```
1.初始化，状态：pending

2.当调用resolve(成功)，状态：pengding=>fulfilled

3.当调用reject(失败)，状态：pending=>rejected
```



## 3promise的优缺点

 优点：

 1.Promise 分离了异步数据获取和业务逻辑，有利于代码复用。

 2.可以采用链式写法

 3.一旦 Promise 的值确定为fulfilled 或者 rejected 后，不可改变。



 缺点：

代码冗余，语义不清。

## 4 为什么用promise？

**一**.**解决回调地狱**

 回调地狱：发送多个异步请求时，每个请求之间相互都有关联，会出现第一个请求成功后再做下一个请求的情况。我们这时候往往会用嵌套的方式来解决这种情况，但是这会形成”回调地狱“。如果处理的异步请求越多，那么回调嵌套的就越深。出现的问题：

1.代码逻辑顺序与执行顺序不一致，不利于阅读与维护。

2.异步操作顺序变更时，需要大规模的代码重构。

3.回调函数基本都是匿名函数，bug追踪困难



**2.解决异步**

我们都知道js是单线程执行代码，导致js的很多操作都是异步执行（ajax）的，以下是解决异步的几种方式：

 1.回调函数(定时器)。

 2.事件监听。

 3.发布/订阅。

 4.Promise对象。(将执行代码和处理结果分开)

 5.Generator。

6.ES7的async/await。



## 5. Promise.all()

多个promise同时使用，其中一个错误会怎样

```
let p1 = Promise.resolve(123);
let p2 = Promise.resolve('hello');
let p3 = Promise.resolve('success');


Promise.all([p1,p2,p3]).then(result => {
    console.log(result); //[ 123, 'hello', 'success' ]
})
```

Promise.all（）成功之后就是数组类型，当所有状态都是成功状态才返回数组，只要其中有一个的对象是reject的，就返回reject的状态值。



```
const pro = (a) => {
    return new Promise((resove,reject)=>{
        if(a==1){
           setTimeout(()=>{
            resove("this is my data")
           },2000)
        }else{
            reject("error data")
        }
    })
}
const pro2 = () => {
    return new Promise((resove,reject)=>{
        reject("error data")
    })
}
Promise.all([pro(1),pro2()]).then((res)=>{
    console.log(res);
    
}).catch((err)=>{
    console.log('走到了catch里面');
    console.log(err); //error data
})
```

因为pro2函数会reject一个错误，所以后面的promise.all调用的函数数组中，会走到catch里面



## 6 Promise.race()

和all同样接受多个对象，不同的是，race()接受的对象中，哪个对象返回的快就返回哪个对象，就如race直译的赛跑这样。如果对象其中有reject状态的，必须catch捕捉到，如果返回的够快，就返回这个状态。race最终返回的只有一个值。

```
//用sleep来模仿浏览器的AJAX请求
function sleep(wait) {
    return new Promise((res,rej) => {
        setTimeout(() => {
            res(wait);
        },wait);
    });
}

let p1 = sleep(500);
let p0 = sleep(2000);

Promise.race([p1,p0]).then(result => {
    console.log(result); // 500
});

let p2 = new Promise((resolve,reject) => {
    setTimeout(()=>{
        reject('error data');
    },1000);
});

Promise.race([p0,p2]).then(result => {
    console.log(result);
}).catch(result => {
    console.log(result); // error data
});
```





## 6 async/await 与 promsie区别

异步编程的最高境界，就是根本不关心它异步，async函数可以说是异步函数的最终解决方案。

async-await与promise不存在谁替换谁的关系，因为async-await是寄生于promise的

基本语法：

```
const pro = (a) => {
    return new Promise((resove,reject)=>{
        if(a==1){
           setTimeout(()=>{
            resove("this is my data")
           },2000)
        }else{
            reject("error data")
        }
    })
}

async function abc(){
    let a = await pro(1)
    console.log(a); // this is my data
    console.log('hello world');
}
abc()
```

async函数返回一个promise对象



规则

1.async表示这是一个async函数，await只能用在这个函数里面

2.await表示在这里等待promise返回结果之后，再继续执行

3.await后面应该跟着一个promise对象（跟普通函数也行，只是时候会立即执行，这样async-await就显得多余了）

4.await必须放在async里面执行

5.await等待的虽然是promise对象，但是不必写.then()，可以直接得到返回结果(例如上面代码执行后，2秒钟之后会打印出a的结果为 this is my data)



## 7 async的错误处理

try-catch捕捉

```
let p = new Promise((resolve,reject) => {
    setTimeout(() => {
        reject('error');
    },1000);
});

async function demo(params) {
    try {
        let result = await p;
    }catch(e) {
        console.log(e);
    }
}

demo();
```





## 8 async-await的优缺点

优点：

1.解决回调地狱的问题

2.语法后面不用再加 `then` 链式回调函数

3.try/catch 使 async 语法的异常捕获更加好用。



缺点：

大多浏览器原生不支持，需要经过babel编译，编译过的代码会变得臃肿