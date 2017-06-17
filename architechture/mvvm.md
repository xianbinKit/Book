# MVVM

### Model

Model 负责展示数据库的数据，将各种数据库格式的数据转成swift的格式。不一定要是struct, 也可以是Core data.

!FILENAME Recipe.swft

```swift
struct Recipe {
  let name: String
  let difficulty: RecipeDifficulty
  let photo: UIImage?
  let photoDescription: String
  let prepTime: Int
  let cookTime: Int
  let yield: Int
  let ingredients: [String]?
  let directions: [String]?
}

extension Recipe {
  init?(dict: [String: AnyObject]) {
    guard let name = dict["name"] as? String,
      let rawDifficulty = dict["difficulty"] as? Int,
      let difficulty = RecipeDifficulty(value: rawDifficulty),
      let prepTime = dict["prepTime"] as? Int,
      let cookTime = dict["cookTime"] as? Int,
      let yield = dict["yield"] as? Int,
      let ingredients = dict["ingredients"] as? [String],
      let directions = dict["directions"] as? [String],
      let photoDescription = dict["photoDescription"] as? String else {
        return nil
    }

    self.name = name
    self.difficulty = difficulty
    self.prepTime = prepTime
    self.cookTime = cookTime
    self.yield = yield
    self.ingredients = ingredients
    self.directions = directions
    self.photoDescription = photoDescription

    if let imageName = dict["imageName"] as? String, !imageName.isEmpty {
      photo = UIImage(named: imageName)
    } else {
      photo = nil
    }
  }
}


// MARK: - Load Sample Data

extension Recipe {
  static func loadDefaultRecipe() -> [Recipe]? {
    return self.loadRecipeFrom("RecipeList")
  }

  static func loadRecipeFrom(_ plistName: String) -> [Recipe]? {
    guard let path = Bundle.main.path(forResource: plistName, ofType: "plist"),
      let array = NSArray(contentsOfFile: path) as? [[String: AnyObject]] else {
        return nil
    }

    return array.map { Recipe(dict: $0) }
      .filter { $0 != nil }
      .map { $0! }
  }
}
```

### ModelView



