## Swift 代码规范



#### 命名

+ 尽量让调用的地方更加简明、省略不必要的单词

+ 驼峰命名法

+ 针对类型和协议首字母大写, 其他首字母小写

+ 工厂方法以 `make` 开头

+ 描述 `一种能力` 的协议以 `-able` 结尾

  ```swift
  // 例如封装 cell 的 reuseidentifier 的生成
  protocol Reusable: class {
      static var reuseIdentifier: String { get }
  }
  
  extension Reusable {
      static var reuseIdentifier: String {
          let cls =  String(describing: self).components(separatedBy: ".").last!
          return cls + "Identifier"
      }
  }
  ```

+ 尽量避免缩写

+ 代理命名, 未命名的第一个参数应该是代理源

  ```swift
  func namePickerView(_ namePickerView: NamePickerView, didSelectName name: String)
  func namePickerViewShouldReload(_ namePickerView: NamePickerView) -> Bool
  ```

+ 使用上下文推断类型

  ```swift
  let selector = #selector(viewDidLoad)
  view.backgroundColor = .red
  let toView = context.view(forKey: .to)
  let view = UIView(frame: .zero)
  ```

+ 布尔值的命名以 `is` 作为前缀

+ 图片命名: 模块+样式+状态

  ```
  home_arrow_n // 普通状态
  home_arrow_h // 高亮
  ```

  

#### 代码组织

每个扩展添加 `// MARK: -` 注释, 保证代码结构清晰

```swift
class MyViewController: UIViewController {
  // 类填充在这
}

// MARK: - UITableViewDataSource
extension MyViewController: UITableViewDataSource {
  // table view 的数据源方法
}

// MARK: - UIScrollViewDelegate
extension MyViewController: UIScrollViewDelegate {
  // scroll view 的代理方法
}
```



#### 空格

+ 用两个字符的缩进, 在 Xcode 的 Text Editing 里面设置
+ 方法大括号 ( `if` / `else` / `switch` 等)，总是在同行写左括号, 新行写右括号

```swift
if user.isHappy {
// 做一件事
} else {
// 做另一件事
}
```

+ 方法之间应该只有一个空行, 方法中的空白应该按功能隔离代码, 一个方法中有很多段意味着需要将他们封装进不同代码
+ 冒号总是在左边没有空格而右边有空格。 特殊情况是三元运算符 `? :` 、空字典 `[:]`  和带有未命名的参数(_:) 的 `#selector` 的语法
+ 每一行的代码不要超过 100 个字符、避免在行结尾增加空白



#### 注释

解释一个特定的代码片段 `为什么` 做某件事



#### 方法声明

一行中保持较短的方法声明, 包括左括号， 较长的声明, 则需要再合适的位置换行

```swift
func reticulateSplines(spline: [Double]) -> Bool {
  
}

func reticulateSplines(spline: [Double], adjustmentFactor: Double,
    translateConstant: Int, comment: String) -> Bool {
  
}

```



#### 常量

尽可能使用枚举描述常量

```
enum Math {
  static let e = 2.718281828459045235360287
  static let root2 = 1.41421356237309504880168872
}

let hypotenuse = side * Math.root2
```



#### 懒加载

```
lazy var locationManager: CLLocationManager = self.makeLocationManager()

private func makeLocationManager() -> CLLocationManager {
  let manager = CLLocationManager()
  manager.desiredAccuracy = kCLLocationAccuracyBest
  manager.delegate = self
  manager.requestAlwaysAuthorization()
  return manager
}
```



#### 内存管理

闭包应该注意避免出现循环引用, 使用惯用的语法 `[weak self]` 和 `guard let strongSelf = self else { return }` 延长对象的生命周期

```swift
resource.request().onComplete { [weak self] response in
  guard let strongSelf = self else {
    return
  }
  let model = strongSelf.updateModel(response)
  strongSelf.updateUI(model)
}
```





#### 访问控制

适时使用 `private` 和 `fileprivate` ，忽略返回值可以使用 `@discardableResult`



#### if 嵌套多层

如果出现这种情况, 可以考虑用 `guard` 改写, 把错误的情况提前 return 

```swift
func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {

  guard let context = context else {
    throw FFTError.noContext
  }
  guard let inputData = inputData else {
    throw FFTError.noInputData
  }

  // 用上下文和输入计算频率
  return frequencies
}
```



#### 尽量避免使用 ！解包