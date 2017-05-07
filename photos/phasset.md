# ios swift PHAsset 获取视频和照片

获取系统图片视频信息

##  针对相机胶卷

##### Fetch all video and photo in Camera Roll,  获取所有存在相机胶卷里的视频和图片

```swift
let allResult = PHAsset.fetchAssets(with: nil)
```

##### 

##### Fetch photos

```swift
let allResult = PHAsset.fetchAssets(with: .image, options: nil)
```



##### Fetch videos

```
let allResult = PHAsset.fetchAssets(with: .video, options: nil)
```



##  针对collection

```swift
let smartAlbums = PHAssetCollection.fetchAssetCollections(with: .smartAlbum, subtype: .smartAlbumUserLibrary, options: nil)
```

 针对不同的type和subtype可以得到不同的collection\(也就是album\).

```swift
let result  = PHAsset.fetchAssets(in: collection, options: nil)
```

 然后再通过对这个collection 进行fetch得到这个collection下的图片和视频。注意这里没有办法过滤是图片还是照片，但是我们可以使用options来过滤，之前的options 都是 nil, 接下来我们将介绍怎么使用它。



## Fetch Options  对照片和视频的结果进行过滤

```swift
let fetchOptions = PHFetchOptions()
// 1
fetchOptions.sortDescriptors = [NSSortDescriptor(key: "creationDate", ascending: false)]
// 2
fetchOptions.predicate = NSPredicate(format: "mediaType == %d || mediaType == %d",
                                             PHAssetMediaType.image.rawValue,
// 3                                             PHAssetMediaType.video.rawValue)
fetchOptions.fetchLimit = 100
```

1. 根据什么规则来排序结果，可以是创建时间，修改时间。。，  ascending 生序还是降序。 
2. 对结果进行过滤。
3. 限制结果的数量。





