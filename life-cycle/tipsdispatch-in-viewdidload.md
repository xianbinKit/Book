# Dispatch in viewDidLoad\(\)

```swift
DispatchQueue.main.async {
            print("dispatch in viewdidload")
}

```

这行信息将打印在viewDidAppear\(\)之后，因为整个流程一开始就已经在队列里了。

