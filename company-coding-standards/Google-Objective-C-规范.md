# Google Objective-C 代码规范

> 官方文档：https://google.github.io/styleguide/objcguide.html

---

## 目录

- [命名规范](#命名规范)
- [代码格式](#代码格式)
- [编程实践](#编程实践)

---

## 命名规范

### 类名

- 使用 **PascalCase**
- 使用前缀避免命名冲突

```objc
// 正确
@interface GTMHttpClient : NSObject
@interface NSMyViewController : UIViewController
```

### 方法名

- 使用 **camelCase**
- 方法名应该描述其功能

```objc
// 正确
- (void)sendMessageWithName:(NSString *)name;
- (NSString *)displayNameForUser:(User *)user;
+ (instancetype)sharedInstance;
```

### 变量

- 使用 **camelCase**

```objc
// 正确
NSString *userName = @"John";
NSInteger itemCount = 10;
```

### 常量

- 使用 **kPascalCase**（k 前缀）

```objc
// 正确
static const NSInteger kMaxItemCount = 100;
static NSString *const kDefaultName = @"Unknown";
```

### 枚举

- 使用 **PascalCase**
- 枚举值使用前缀

```objc
// 正确
typedef NS_ENUM(NSInteger, GTMHttpStatus) {
    GTMHttpStatusOK = 200,
    GTMHttpStatusNotFound = 404,
    GTMHttpStatusError = 500,
};
```

---

## 代码格式

### 缩进

- 使用 **2 个空格**

### 大括号

- 左大括号放在同一行

```objc
// 正确
if (condition) {
    [self doSomething];
} else {
    [self doSomethingElse];
}
```

### 方法调用

```objc
// 正确
[self doSomethingWithObject:object];

// 多参数换行
[self doSomethingWithObject:object
                   parameter:param
                   completion:^{
    // completion block
}];
```

### 属性

```objc
// 正确
@interface MyClass : NSObject

@property (nonatomic, copy) NSString *userName;
@property (nonatomic, assign) NSInteger itemCount;
@property (nonatomic, weak) id<MyDelegate> delegate;

@end
```

---

## 编程实践

### 使用 @property

- 优先使用 @property 而非实例变量

```objc
// 正确
@interface MyClass : NSObject
@property (nonatomic, copy) NSString *name;
@end

// 错误
@interface MyClass : NSObject {
    NSString *_name;
}
@end
```

### 使用字面量语法

```objc
// 正确
NSArray *array = @[@1, @2, @3];
NSDictionary *dict = @{@"key": @"value"};
NSNumber *number = @42;

// 错误
NSArray *array = [NSArray arrayWithObjects:@1, @2, @3, nil];
```

### 使用 block

```objc
// 正确
[self fetchItemsWithCompletion:^(NSArray *items, NSError *error) {
    if (error) {
        [self handleError:error];
        return;
    }
    [self processItems:items];
}];
```

---

## 参考资料

- [Google Objective-C Style Guide (官方)](https://google.github.io/styleguide/objcguide.html)

---

*本文档基于 Google Objective-C Style Guide 整理*
