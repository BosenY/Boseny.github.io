---
title: 初学RxJS
date: 2017-03-20 08:34:42
tags:
---
## 初学Rxjs

### 概念

Rxjs 是一个通过使用可观察序列来构建异步和基于事件的程oberservable序的库，可以吧它当成一个针对于事件的lodash


Rxjs就是JavaScript的响应式扩展，响应式的思路就是把随时间不断变化的数据、状态、事件等等转化成可被观察的序列(observable sequence),然后订阅序列中那些observable对象的变化，一旦变化，就会执行事先安排好的各种转换和操作


### 四个生命周期 

* 创建：创建一个observable，返回一个被观察的序列源实例
* 订阅：通过序列源实例可以订阅序列发射新数据变更时的响应方法（回调方法）
* 执行：响应的动作就是执行
* 销毁：通过序列源实例可以销毁，而当订阅方法发生错误时也会自动销毁

### 剖析可观察对象
使用Rx.Observable.create或一个能产生可观察对象的操作符来创造一个可观察对象，使用一个观察者订阅他，执行然后给观察者发送next/error/complete的通知，他们的执行可能会被disposed（处理）。这四个方面均被编码进可观察对象的实例当中。

## 核心的可观察对象的概念

* Creating Observables 创建
* Subscribing Obserables 订阅
* Executing the Observable 执行
* Disposing Observables 处理


### Creating Observables
Rx.Observable.create 用来创建一个可观察对象 ，是可观察对象构造函数的别名，它接受一个参数（订阅的 fnuction）

```javascript
var observable = Rx.Observable.create(function subscribe(observer) {
    var id = setInterval(() => {
    observer.next('hi')
    }, 1000);
});
```

### Subscribing Obserables

一个可观察对象可以被订阅

```javascript
observable.subscribe(x => console.log(x));
```

这里的subscribe和上面create的subscribe是不一样的，但是你可以在概念上将他们等价，上面写成一个匿名函数也是可以的
```javascript
var observable = Rx.Observable.create(observer => {
    var id = setInterval(() => {
    observer.next('hi')
    }, 1000);
});
```

    订阅一个可观察对象就像是调用一个函数，在数据将被发送的地方提供回调

完全不同于addEventListener/removeEventListener事件句柄API,使用observervable.subscribe，给定的观察者并没有作为一个监听者被注册

订阅数启动可观察对象执行和发送值或者事件给观察者的简单方式

### Executing the Observable
执行可观察对象就是在创建时里面的匿名函数做的事情，一个仅在观察者订阅时发生的惰性计算，执行随时间产生多个值，以同步或者异步的方式

下面是observervable对象可以发送的三种类型的值：
1. next 发送一个数字/字符串/对象等等
2. error 发送一个js错误或者异常
3. complete 不发送值
next可以在可观察对象执行期间发生多次，而error和complete只能在执行期间发生一次，但仅会执行二者之中的一个

        一个可观察对象的执行期间，零个到无穷多个next通知被发送。如果Error或者Complete通知一旦被发送，此后将不再发送任何值。

一个好的使用方式就是使用try catch语句去包裹通知语句，如果捕获了异常就会发送一个错误通知

```javascript
var observable = Rx.Observable.create(function subscribe(observer) {
try {
observer.next(1);
observer.next(2);
observer.next(3);
observer.complete();
} catch (err) {
observer.error(err); // delivers an error if it caught one
}
});
```
### Disposing Observables
处理可观察对象的执行：
    由于可观察对象的执行可能是无限的(无数个next)，而对于观察者来说却往往需要在有限的时间内终止执行，因此需要一个api来取消执行。因为每次的执行仅仅服务于一个观察者，一旦观察者听得接收数据，他就不得不通过一个方式去终止执行，从而避免浪费大量的计算性能和内存资源

这里observable.subscribe被调用返回了一个对象： subscription
这个对象表示了正在进行的执行：

```javascript
var subscription = observable.subscribe(x => console.log(x));
```

在这里使用subscription.unsubscribe()就可以取消你正在进行的执行


## observer观察者

观察者就是可观察对象所发送数据的消费者，简单说就是一组回调函数，分别对应一种被可观察对象发送的通知的类型：next、error和complete

    观察者不过是三个回调函数组成的对象，每个回调函数分别对应可观察对象的通知类型

```javascript
var observer={
next:x=>console.log('Observer got a next value: ' + x),
error: err => console.error('Observer got an error: ' + err),
complete: () => console.log('Observer got a complete notification')
}
observable.subscribe(observer)
```
当订阅一个可观察对象，你仅仅提供回调来作为参数就够了，并不需要完整的观察者对象

在observable.subscribe内部，他讲使用第一个回调参数作为next的处理句柄创建一个观察者对象，也可以通过将三个函数作为参数提供三种回调


```javascript
observable.subscribe(
    x => console.log('Observer got a next value: ' + x),
    err => console.error('Observer got an error: ' + err),
    () => console.log('Observer got a complete notification')
);
```

## Subject主题

Subject是允许值被多播到多个观察者的一种特殊的observable

Subject就是一个可观察对象，只不过可以被多播至多个观察者。同时Subject也类似于eventemitter：维护着众多事件监听器的注册表

* 每一个Subject及时一个可观察对象，又是一个观察者对象，也就是说，它既可以拥有next、error、complete方法，又可以去subscribe它
* 观察者： 有next、error等方法
* 可观察对象： 可以被订阅
demo： 

```javascript
var subject = new Rx.Subject();

subject.subscribe({
  next: (v) => console.log('observerA: ' + v)
});
subject.subscribe({
  next: (v) => console.log('observerB: ' + v)
});

subject.next(1);
subject.next(2);
```
输出效果如下：
```javascript
observerA: 1
observerB: 1
observerA: 2
observerB: 2
```


### 多播的可观察对象

一个多播的可观察对象可以通过多个订阅者的订阅去传递通知，而普通的单播可观察对象不可以
```javascript
var source=Rx.Observable.from([1,2,3]);
var subject=new Rx.Subject();
var multicasted=source.multicast(subject);
multicasted.subscribe({
  next:(v)=>console.log('observerA:' +v);
});
multicasted.subscribe({
  next: (v) => console.log('observerB: ' + v)
});
multicasted.connect();
```
multicast方法返回一个看起来像普通的可观察对象的可观察对象，但是却有着和subject一样的行为，multicast返回一个connectableobservable，他是一个具有connect方法的observable

connect方法对于觉得何时开始分享可观察对象的执行时非常重要的，在source下面有source.subscribe（subject），connect（）返回一个Subscription，你可以取消订阅，以取消共享的Observable执行。