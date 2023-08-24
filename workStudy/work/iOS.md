### 打包发布到 TestFlight 的流程

1. **构建应用程序：**
   - 在 Xcode 中，选择通用设备，然后使用 Archive 选项构建的应用程序。
2. **创建 Archive：**
   - 在 Xcode 的 Organizer 中，选择应用程序，然后点击 "Distribute App"。
3. **选择分发方法：**
   - 选择 "iOS App Store" 作为分发方法，即将应用程序上传到 App Store Connect。

当在 Xcode 中进行应用程序发布时，第三步选择分发方法后，会进入一个设置和配置的阶段。这个阶段包含了一些选择配置项，让你为你的应用程序设置发布相关的详细信息。以下是这个阶段中的一些选择配置项的详细介绍：

2. **Distribute App 或 Manually Manage Signing：**
   - 选择 "Distribute App" 来自动管理证书和签名，Xcode 将自动为你签名应用程序。
   - 选择 "Manually Manage Signing" 以手动管理证书和签名，你需要在后续步骤中手动选择发布证书和描述文件。

3. **选择发布证书：**
   - 如果选择了 "Distribute App"，Xcode 将自动为你选择发布证书。如果选择了 "Manually Manage Signing"，你需要从下拉列表中选择发布证书。

4. **选择描述文件：**
   - 如果选择了 "Distribute App"，Xcode 将自动为你选择适用的描述文件。如果选择了 "Manually Manage Signing"，你需要从下拉列表中选择适用的描述文件。

5. **Export Compliance：**
   - 这个步骤涉及到关于加密、出口控制等法规要求的信息。根据你的应用程序特性，选择适用的选项。

6. **Bitcode：**
   - Bitcode 是一种编译中间码，允许 App Store 动态优化你的应用程序。根据你的需求，选择是否包括 Bitcode。

7. **Symbolicate Checked Builds：**
   - 如果启用这个选项，Xcode 会将崩溃报告的符号化信息上传到 Apple，以便你在 Xcode 中查看崩溃日志。

8. **Include manifest for over-the-air installation：**
   - 如果你希望支持通过网络（OTA）安装应用程序，请启用这个选项。

9. **Automatically manage signing：**
   - 如果选择 "Distribute App" 并启用这个选项，Xcode 将自动管理证书和签名。

10. **Upload your app’s symbols to receive symbolicated reports from Apple：**
    - 如果启用这个选项，Xcode 会上传应用程序的符号化信息，以便 Apple 提供符号化的崩溃报告。



### iOS Object-c：

#### 1. **类的定义和声明：**

Objective-C 使用 `@interface` 和 `@implementation` 来定义和实现类。

```objective-c
// 声明类接口
@interface Person : NSObject

// 属性和方法声明
@property (nonatomic, strong) NSString *name;
- (void)sayHello;

@end

// 实现类
@implementation Person

@synthesize name;

- (void)sayHello {
    NSLog(@"Hello, %@", self.name);
}

@end
```

#### 2. **方法：**

Objective-C 使用 `-` 表示实例方法，使用 `+` 表示类方法。

```objective-c
// 实例方法
- (void)performAction {
    // 实例方法的实现
}

// 类方法
+ (void)printMessage {
    // 类方法的实现
}
```

#### 3. **属性：**

使用 `@property` 来声明属性，自动生成 Getter 和 Setter 方法。

```objective-c
@property (nonatomic, strong) NSString *name;
@property (nonatomic, assign) NSInteger age;
```

#### 4. **对象的创建与使用：**

使用 `[[Class alloc] init]` 来创建对象，使用点语法访问属性和方法。

```objective-c
Person *person = [[Person alloc] init];
person.name = @"John";
[person sayHello];
```

#### 5. **基本数据类型：**

Objective-C 支持 C 语言的基本数据类型，如整数、浮点数、字符等。

```objective-c
int number = 10;
float floatValue = 3.14;
char character = 'A';
```



###  `.h` 和 `.m` 文件：

在 Objective-C 中，`.h` 和 `.m` 文件是用于定义和实现类的两个关键文件。这些文件一起构成了类的声明和实现，允许在 Objective-C 中创建和使用类。

#### `.h` 文件（Header 文件）

`.h` 文件通常被称为头文件（Header 文件），它包含了类的公共接口和声明。这个文件定义了其他代码如何与类进行交互。

1. **类声明：** 使用 `@interface` 关键字来声明类。

   ```objective-c
   @interface MyClass : NSObject

   // 声明属性和方法

   @end
   ```

2. **属性声明：** 使用 `@property` 关键字声明属性，包括数据类型和访问修饰符。

   ```objective-c
   @interface MyClass : NSObject

   @property (nonatomic, strong) NSString *name;
   @property (nonatomic, assign) NSInteger age;

   @end
   ```

3. **方法声明：** 声明实例方法和类方法，用于暴露类的行为。

   ```objective-c
   @interface MyClass : NSObject

   - (void)doSomething;
   + (void)doSomethingStatic;

   @end
   ```

4. **协议声明：** 可以在头文件中声明类遵循的协议。

   ```objective-c
   @interface MyClass : NSObject <MyProtocol>

   // ...

   @end
   ```

#### `.m` 文件（Implementation 文件）

`.m` 文件包含了类的实现，定义了类中各个方法的具体代码。

1. **导入头文件：** 使用 `#import` 导入与类相关的头文件。

   ```objective-c
   #import "MyClass.h"
   ```

2. **类实现：** 使用 `@implementation` 关键字来实现类。

   ```objective-c
   @implementation MyClass

   // 实现方法和属性的具体代码

   @end
   ```

3. **方法实现：** 实现声明在头文件中的方法。

   ```objective-c
   @implementation MyClass

   - (void)doSomething {
       // 实现代码
   }

   + (void)doSomethingStatic {
       // 实现代码
   }

   @end
   ```

4. **属性合成：** 可以使用 `@synthesize` 或自动合成特性来生成属性的 Getter 和 Setter 方法。

   ```objective-c
   @implementation MyClass

   @synthesize name;

   // 或者使用自动合成
   @synthesize age = _age;

   @end
   ```

这些是 Objective-C 中 `.h` 和 `.m` 文件的基本组成部分。`.h` 文件定义了类的接口和公共部分，而 `.m` 文件包含了类的实现和私有方法。