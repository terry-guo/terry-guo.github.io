---
title: React生命周期
date: 2018-10-07 19:16:08
tags:
---

​	一直没有梳理过react中的生命周期，因为平时常用的生命周期就那么几个，今天就系统的了解一下react中用到的生命周期。

​	下面看一下一个组件的基本构造。

~~~
import React,{ Component } from 'react';

class NewDemo extends Component {
  constructor(props,context) {
      super(props,context)
      this.state = {
          //定义state
      }
  }
componentWillMount () {
}
componentDidMount () {
}
componentWillReceiveProps (nextProps) {
}
shouldComponentUpdate (nextProps,nextState) {
}
componentWillUpdate (nextProps,nextState) {
}
componentDidUpdate (prevProps,prevState) {
}
render () {
    return (
        <div></div>
    )
}
componentWillUnmount () {
}
}
export default NewDemo;
~~~



- React 16.3 新增的生命周期方法

  ​	1.getDerivedStateFromProps()

  ​	2.getSnapshotBeforeUpdate()

  

- 逐渐废弃的生命周期方法：

  ​	1.componentWillMount()

  ​	2.componentWillReceiveProps()

  ​	3.componentWillUpdate()

# 1.constructor

react组件的构造函数在挂载之前被调用。在实现`React.Component`构造函数时，需要先在添加其他内容前，调用`super(props)`，用来将父组件传来的`props`绑定到这个类中，使用`this.props`将会得到。

官方建议不要在`constructor`引入任何具有副作用和订阅功能的代码，这些应当在`componentDidMount()`中写入。

`constructor`中应当做些初始化的动作，如：初始化`state`，将事件处理函数绑定到类实例上，但也不要使用`setState()`。如果没有必要初始化state或绑定方法，则不需要构造`constructor`，或者把这个组件换成纯函数写法。

​	constructor参数接受两个参数props,context 可以获取到父组件传下来的的props,context,如果你想在		constructor**构造函数内部(注意是内部哦，在组件其他地方是可以直接接收的)**使用props或context,则需要传入，并传入super对象。 

~~~
 constructor(props,context) {
  super(props,context)
  console.log(this.props,this.context) // 在内部可以使用props和context
}
~~~

1 constructor必须用super()初始化this, 可以绑定事件到this

2 如果你在constructor中要使用this.props, 就必须给super加参数, super(props)；

3 无论有没有constructor, render中都可以使用this.props, 默认自带

4 如果组件没有声明constructor, react会默认添加一个空的constructor 

5 ES6采用的是先创建父类的实例this（故要先调用 super( )方法），完后再用子类的构造函数修改this



# 2.componentWillMount （组件将要挂载）

1、组件刚经历constructor,初始完数据 

2、组件还未进入render，组件还未渲染完成，dom还未渲染 

componentWillMount 一般用的比较少，更多的是用在服务端渲染，（我还未使用过react服务端渲染哈，所以也写不了很多） 

但是有一点需要注意的，一般ajax请求不要在这个生命周期里面进行，虽然有些情况下并不会出错，但是如果ajax请求过来的数据是空，那么会影响页面的渲染，可能看到的就是空白。 



# 3.componentDidMount（组件渲染完成） 

组件完成装载（已经插入 DOM 树）时，触发该方法。组件第一次渲染完成，此时dom节点已经生成，可以在这里调用ajax请求，返回数据setState后组件会重新渲染 。 

一般用于下面场景

> 1.异步请求 ajax
> 2.添加事件绑定（注意在 componentWillUnmount 中取消，以免造成内存泄漏）



# 4.componentWillReceiveProps (nextProps)

componentWillReceiveProps在接受父组件改变后的props需要重新渲染组件时用到的比较多 

~~~
class ExampleComponent extends React.Component {
  state = {
    isScrollingDown: false,
  };
 
  componentWillReceiveProps(nextProps) {
    if (this.props.currentRow !== nextProps.currentRow) {
      this.setState({
        isScrollingDown:nextProps.currentRow
      });
    }
  }
}
~~~

这个方法将被弃用，推荐使用 getDerivedStateFromProps 代替。 

# 5.shouldComponentUpdate(nextProps,nextState)

​	返回一个布尔值。 

​	唯一用于控制组件重新渲染的生命周期，由于在react中，setState以后，state发生变化，组件会进入重新渲染的流程，（暂时这么理解，其实setState以后有些情况并不会重新渲染，比如**数组引用不变**）在这里return false可以阻止组件的更新
	 该方法通过返回 true 或者 false 来确定是否需要触发新的渲染。返回 false， 则不会触发后续的 componentWillUpdate()、render() 和 componentDidUpdate()（但是 state 变化还是可能引起子组件重新渲染）。

所以通常通过这个方法对 props 和 state 做比较，从而避免一些不必要的渲染。

 

# 6.componentWillUpdate (nextProps,nextState)

shouldComponentUpdate返回true以后，组件进入重新渲染的流程，进入componentWillUpdate,这里同样可以拿到nextProps和nextState 。这个平时倒是用的不多。



# 7.render函数

**用于将模板转为 HTML 语言，并插入指定的 DOM 节点。** 

render函数会插入jsx生成的dom结构，react会生成一份虚拟dom树，在每一次组件更新时，在此react会通过其diff算法比较更新前后的新旧DOM树，比较以后，找到最小的有差异的DOM节点，并重新渲染 

 ~~~
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('example')
);
 ~~~

上面代码将一个 h1 标题，插入 example 节点，输出一个h1标签的Hello, world!

 

# 8.componentDidUpdate

在组件完成更新后立即调用。在初始化时不会被调用。 

组件一次重新渲染的过程，下面5处打印出来的state应该是相同的。 

~~~
componentWillReceiveProps (nextProps,nextState) {
    this.setState({
        fengfeng:nextProps.fengfeng
    },()=>{
        console.log(this.state.fengfeng) //1
    })
    
}
shouldComponentUpdate (nextProps,nextState) {
    console.log(nextState.fengfeng)  //2
}
componentWillUpdate (nextProps,nextState) {
    console.log(nextState.fengfeng)  //3
}
componentDidUpdate (prevProps,prevState) {
    console.log(this.state.fengfeng) //5
}
render () {
    console.log(this.state.fengfeng) //4
    return (
        <div></div>
    )
}
~~~



 # 9.componentWillUnmount 

在组件从 DOM 中移除之前立刻被调用。 

componentWillUnmount也是会经常用到的一个生命周期 

> 1.clear你在组建中所有的setTimeout,setInterval 
>
> 2.移除所有组建中的监听 removeEventListener 
>
> 3.也许你会经常遇到这个warning: 

~~~
Can only update a mounted or mounting component. This usually means you called setState() on an       
 unmounted component. This is a no-op. Please check the code for the undefined component.
~~~

实际的原因是因为在组件挂载（mounted）之后进行了异步操作，比如ajax请求或者设置了定时器等，而你在callback中进行了setState操作。当你切换路由时，组件已经被卸载（unmounted）了，此时异步操作中callback还在执行，请求还未完成，setState没有得到值。因此会报warning 。

> 我一般是这么解决的

~~~
   componentWillUnmount() {
        //重写组件的setState方法，直接返回空
        this.setState = (state, callback) => {
            return;
        };
    }
~~~

> 其实还有两种解决方法
>
> 1、**在卸载的时候对所有的操作进行清除（例如：abort你的ajax请求或者清除定时器）** 

~~~
componentDidMount () {
    //1.ajax请求
    $.ajax('你的请求',{})
        .then(res => {
            this.setState({
                aa:true
            })
        })
        .catch(err => {})
    //2.定时器
    timer = setTimeout(() => {
        //dosomething
    },1000)
}
componentWillUnMount  () {
    //1.ajax请求
    $.ajax.abort()
    //2.定时器
    clearTimeout(timer)
}
~~~

> 2、**设置一个flag，当unmount的时候重置这个flag** 

~~~
componentDidMount () {
    this._isMounted = true;
    $.ajax('你的请求',{})
        .then(res => {
            if(this._isMounted){
                this.setState({
                    aa:true
                })
            }
        })
        .catch(err => {})
}
componentWillUnMount () {
    this._isMounted = false;
}

~~~

不过根据我的实际经验，还是重写组件的setState方法最管用。



# 10.React16新增的生命周期

## 10-1.getDerivedStateFromProps

`getDerivedStateFromProps`在组件实例化后，和接受新的`props`后被调用。他返回一个对象来更新状态，或者返回null表示新的props不需要任何state的更新。

如果是由于父组件的props更改，所带来的重新渲染，也会触发此方法。

调用`steState()`不会触发`getDerivedStateFromProps()`。



## 10-2、getSnapshotBeforeUpdate

~~~
 getSnapshotBeforeUpdate(prevProps, prevState) {
    // ...
  }
~~~

新的`getSnapshotBeforeUpdate`生命周期在更新之前被调用（例如，在DOM被更新之前）。此生命周期的返回值将作为第三个参数传递给`componentDidUpdate`。 （这个生命周期不是经常需要的，但可以用于在恢复期间手动保存滚动位置的情况。）

与`componentDidUpdate`一起，这个新的生命周期将覆盖旧版`componentWillUpdate`的所有用例。



# 11.生命周期各函数的调用顺序



![img](React生命周期\react-01.jpg)



1. `getDefaultProps()`，调用1次
2. `getInitialState()`，调用1次
3. `componentWillMount()`，调用1次
4. `render()`，调用>=1次
5. `componentDidMount()`：仅客户端，调用1次
6. `componentWillReceiveProps(object nextProps)`，调用>=0次
7. `ShouldComponentUpdate(object nextProps, object nextState)`，调用>=0次
8. `componentWillUpdate(object nextProps, object nextState)`，调用>=0次
9. `render()`，调用>=1次
10. `componentDidUpdate(object prevProps, object prevState)`，调用>=0次
11. `componentWillUnmount()`，调用1次

