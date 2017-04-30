# SwiftyJSON 使用

##### Install with cocoapods

```
pod 'SwiftyJSON'
```

##### 

##### Create JSON object from a JSON file

```swift
let url = Bundle.main.url(forResource: "users", withExtension: "json")
guard let data = try? Data(contentsOf: userJsonURL) else { return } // deal with nil 
let json = JSON(data: data)
// handle your json obejct
```

##### 

##### Create JSON object from http download

```swift
// http request for JSON file
        URLSession.shared.dataTask(with:url!) {
            (jsonData, response, error) in
            guard error == nil else {
                print(error!.localizedDescription)
                return
            }
            guard let jsonData = jsonData else {
                print("json data nil")
                return
            }
            let json = JSON(data : jsonData)
            // handle your json obejct
        }.resume()
```

##### Create JSON from string

```swift
if let dataFromString = jsonString.data(using: .utf8, allowLossyConversion: false) {
    let json = JSON(data: dataFromString)
}
```

##### JSON object 的类型

JSON 可以是一个字典，也可以是一个数组。字典以 "key"-JSON形式出现，数组以index-JSON形式出现。在没有展开数值之前，读取到的都是JSON object, 即使是一个简单的 `"id" : 3` 也是一个JSON.

```
{
    "id" : 1,             // key - int,double
    "title" : "spot 1"    // key - string
    "coordinate" :        // key - array
    [
        2.113,
        3.2323
    ],
}

json["id"]                   // is a JSON(1)
json["title"]                // is a JSON("spot 1")
json["coordinate"]            // is a Array[JSON(2.113),JSON(3.2323)]
```

JSON遍历

```swift
//If json is .Dictionary
for (key,subJson):(String, JSON) in json {
   //Do something you want
}

//If json is .Array
//The `index` is 0..<json.count's string value
for (index,subJson):(String, JSON) in json {
    //Do something you want
}
```

当然不是所有时候我们都需要key或者index的值，我们可以用\_替换，也可以直接拿到subJson的数组.

```swift
json["coordinate"].array        // 返回一个[JSON]?
json["coordinate"].arrayValue    // 返回一个[JSON]

// 所以我们也可以用map来处理数组
json["coordinate"].arrayValue.map{$0}
```

##### Option值和non-Option值

swiftyJSON很方便的处理这两种值。

区别就在于 `string`和 `stingValue`.

```swift
// Option
if let id = json["user"]["favourites_count"].number {
   //Do something you want
} else {
   //Print the error
   print(json["user"]["favourites_count"].error)
}

// Non-Option
let id = json["user"]["favourites_count"].numberValue
```

在读取Non-Option值时，如果值为nil，将会给一个默认值。一下是对应表。

| 类型 | Option | Non-Option | 默认值 |
| :--- | :--- | :--- | :--- |
| String | .string | .stingValue | "" |
| NSNumber | .number | .numberValue | 0 |
| Int | .int | .intValue | 0 |
| Double | .double | .doubleValue | 0.0 |
| Array | .array | .arrayValue | \[\] |

##### json 读取

可以知道，json只有 key-value或则index-value两种形式，所以可以像下面这样取到想要的值。

```swift
//Just the same
let name = json[1]["list"][2]["name"].string
//Alternatively
let name = json[1,"list",2,"name"].string
```

### JSON 文件格式

```
{
    "id" : 1,             // key - int,double
    "title" : "spot 1"    // key - string
    "coordiante" :        // key - array
    [
        2.113,
        3.2323
    ],
    "info" : "more info",
    "newJSON" :
    [
        {
            "id" : 11,
            "title" : "title11"
        },
        {
            "id" : 12,
            "title" : "title12"
        }
    ]

}
```

json都是以key-value形式出现的，值可以是数字，字符串，也可以是数组，数组里面的值可以是数字，字符串，数组，甚至是另一个json。



### [JSONSerialization](https://developer.apple.com/reference/foundation/nsjsonserialization) VS [SwiftyJSON](https://github.com/SwiftyJSON/SwiftyJSON)



苹果官方的例子 ： https://developer.apple.com/swift/blog/?id=37





