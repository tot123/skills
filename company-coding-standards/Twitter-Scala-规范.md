# Twitter Scala 代码规范

> 官方文档：https://twitter.github.io/effectivescala/

---

## 目录

- [格式化](#格式化)
- [类型与泛型](#类型与泛型)
- [集合](#集合)
- [并发编程](#并发编程)
- [函数式编程](#函数式编程)
- [面向对象编程](#面向对象编程)
- [错误处理](#错误处理)

---

## 格式化

### 缩进

- 使用 **2 个空格**

```scala
// good
def foo() = {
  val x = 1
  x
}
```

### 行长度

- 最大 **100** 个字符

### 空格

- 运算符两侧加空格

```scala
// good
val x = 1 + 2
val list = List(1, 2, 3)
```

### 大括号

- 左大括号放在同一行

```scala
// good
if (condition) {
  doSomething()
} else {
  doSomethingElse()
}
```

---

## 类型与泛型

### 使用类型推断

```scala
// good
val list = List(1, 2, 3)

// bad
val list: List[Int] = List(1, 2, 3)
```

### 为公共 API 添加类型注解

```scala
// good
def add(a: Int, b: Int): Int = a + b
```

### 使用类型别名

```scala
// good
type UserId = Long
type UserName = String
```

---

## 集合

### 使用不可变集合

```scala
// good
val list = List(1, 2, 3)
val map = Map("a" -> 1, "b" -> 2)
val set = Set(1, 2, 3)
```

### 使用集合操作

```scala
// good
val doubled = list.map(_ * 2)
val filtered = list.filter(_ > 0)
val summed = list.sum
```

### 避免使用 var

```scala
// bad
var sum = 0
list.foreach(x => sum += x)

// good
val sum = list.sum
```

---

## 并发编程

### 使用 Future

```scala
import scala.concurrent.Future
import scala.concurrent.ExecutionContext.Implicits.global

// good
def fetchData(): Future[Data] = Future {
  // fetch data
}

def process(): Future[Result] = {
  fetchData().map { data =>
    // process data
  }
}
```

### 避免阻塞

```scala
// bad
val result = Await.result(future, 10.seconds)

// good
future.onComplete {
  case Success(value) => // handle success
  case Failure(error) => // handle error
}
```

---

## 函数式编程

### 使用高阶函数

```scala
// good
val result = list
  .filter(_ > 0)
  .map(_ * 2)
  .take(10)
```

### 使用模式匹配

```scala
// good
def describe(x: Any): String = x match {
  case 0 => "zero"
  case n: Int => s"positive number: $n"
  case s: String => s"string: $s"
  case _ => "unknown"
}
```

### 使用 case class

```scala
// good
case class User(id: Long, name: String, email: String)
```

---

## 面向对象编程

### 使用 trait

```scala
// good
trait Repository[T] {
  def findById(id: Long): Option[T]
  def save(entity: T): T
  def delete(id: Long): Unit
}
```

### 使用伴生对象

```scala
// good
class User(val id: Long, val name: String)

object User {
  def apply(name: String): User = {
    new User(generateId(), name)
  }
}
```

---

## 错误处理

### 使用 Option

```scala
// good
def findUser(id: Long): Option[User] = {
  // find user
}

val name = findUser(1).map(_.name).getOrElse("unknown")
```

### 使用 Try

```scala
import scala.util.{Try, Success, Failure}

// good
def parseNumber(s: String): Try[Int] = Try(s.toInt)

parseNumber("123") match {
  case Success(n) => println(s"Number: $n")
  case Failure(e) => println(s"Error: ${e.getMessage}")
}
```

### 使用 Either

```scala
// good
def divide(a: Int, b: Int): Either[String, Int] = {
  if (b == 0) Left("division by zero")
  else Right(a / b)
}
```

---

## 参考资料

- [Effective Scala (官方)](https://twitter.github.io/effectivescala/)
- [Effective Scala 中文版](https://twitter.github.io/effectivescala/index-cn.html)

---

*本文档基于 Twitter Effective Scala 整理*
