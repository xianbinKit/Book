# Bundle/Document 读取

读取main Bundle下的文件：

!FILENAME testBundle.swift

```
let url = Bundle.main.url(forResource: "CES2014", withExtension: "mov")
let path = Bundle.main.path(forResource: "CES2014", withExtension: "mov")
```

读取document下的文件：

!FILENAME testDocument.swift

```
let paths = FileManager.default.urls(for: .documentDirectory, in: .userDomainMask)    
let documentsDirectory = paths[0]
```



