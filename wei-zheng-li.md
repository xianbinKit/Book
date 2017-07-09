##### Swift   weak和unowned

[http://swifter.tips/retain-cycle/](http://swifter.tips/retain-cycle/)

简单的说就是weak会进行强引用检测，效率比unowened低，但是不会奔溃。比如发送一个网络请求，在请求返回时修改一个label的值，所以这个label被这个网络请求的闭包引用了，如果在网络请求返回之前，这个label所属的viewcontroller被消除了（用户不等待网络操作了，切换到了其他页面），那么这时候用unowned就会奔溃。



#####  如何优化swift代码性能

https://juejin.im/entry/56b60c97816dfa005ae0c0d4



