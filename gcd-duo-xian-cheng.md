# GCD 多线程

##### Concurrent Queue

```
let concurrentQueue = DispatchQueue(label: "queuename", attributes: .concurrent)
concurrentQueue.sync{
}
```

##### Serial Queue

```
let serialQueue = DispatchQueue(label: "queuename")
serialQueue.sync{
}
```

##### Main Queue

```
DispatchQueue.main.async{
}
```

```
DispatchQueue.main.sync {
}
```

##### Background Queue

    DispatchQueue.global(qos: DispatchQoS.QoSClass.default).async {
    }

    DispatchQueue.global().async {
        // qos' default value is ´DispatchQoS.QoSClass.default`
    }



