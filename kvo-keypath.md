# ios Swift KVO KeyPath _**观察者设计模式**_

原理 : [http://www.jianshu.com/p/e59bb8f59302](http://www.jianshu.com/p/e59bb8f59302)

总结：

假设有一个类Person, Person有一个属性age. 当加入观察者模式时，其实是创建了一个Person的子类，然后替换掉了age属性的willSet和didSet方法。来实现的通知。

