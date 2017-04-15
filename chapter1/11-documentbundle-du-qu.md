# 1.1 Document/Bundle 读取

!FILENAME testBundle.swift

```Swift
let url = Bundle.main.url(forResource: "CES2014", withExtension: "mov")
let path = Bundle.main.path(forResource: "CES2014", withExtension: "mov")
```



!FILENAME testDocument.swift

```
let paths = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)
let documentsDirectory = paths[0]
```



