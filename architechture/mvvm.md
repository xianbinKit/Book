# MVVM

### Model

Model 负责展示数据库的数据，将各种数据库格式的数据转成swift的格式。不一定要是struct, 也可以是Core data. Model数据通常是全app唯一的，方便数据库统一管理和更新。

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

### ViewModel

ModelView将Model的数据经过处理后提供给不同的View，并不是所有的View都需要ViewModel, 一些简单的Model也可以直接被View加载。



```swift


import Foundation

enum RecipeInstructionType {
  case ingredient, cookingInstructions
}

struct InstructionViewModel {
  let recipe: Recipe?
  var type: RecipeInstructionType
  var ingredientsState = [Bool]()
  var directionsState = [Bool]()
  
  init(recipe: Recipe, type: RecipeInstructionType) {
    self.recipe = recipe
    self.type = type
    
    if let ingredients = recipe.ingredients {
      ingredientsState = [Bool](repeating: false, count:ingredients.count)
    }
    
    if let directions = recipe.directions {
      directionsState = [Bool](repeating: false, count:directions.count)
    }
  }
  
  mutating func numberOfItems() -> Int {
    
    switch type {
    case .ingredient:
      if let ingredients = recipe?.ingredients {
        return ingredients.count
      }
    case .cookingInstructions:
      if let directions = recipe?.directions {
        return directions.count
      }
    }
    
    return 0
  }
  
  func numberOfSections() -> Int {
    return 1
  }
  
  func itemFor(_ index: Int) -> String? {
    switch type {
    case .ingredient:
      if let ingredients = recipe?.ingredients {
        return ingredients[index]
      }
    case .cookingInstructions:
      if let directions = recipe?.directions {
        return directions[index]
      }
    }
    return nil
  }
  
  func getStateFor(_ index: Int) -> Bool {
    switch type {
    case .ingredient:
      return ingredientsState[index]
    case .cookingInstructions:
      return directionsState[index]
    }
  }
  
  mutating func selectItemFor(_ index: Int) {
    switch type {
    case .ingredient:
      let previousState = ingredientsState[index]
      ingredientsState[index] = !previousState
    case .cookingInstructions:
      let previousState = directionsState[index]
      directionsState[index] = !previousState
    }
  }
}

```



