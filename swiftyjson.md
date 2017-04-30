# SwiftyJSON 使用

##### Create JSON object from a JSON file

```swift
let url = Bundle.main.url(forResource: "users", withExtension: "json")
guard let data = try? Data(contentsOf: userJsonURL) else { return } // deal with nil 
let json = JSON(data: data)
// handle your json obejct
```



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



