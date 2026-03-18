# Alibaba Java 开发手册

> GitHub: https://github.com/alibaba/p3c

---

## 目录

- [命名风格](#命名风格)
- [常量定义](#常量定义)
- [代码格式](#代码格式)
- [OOP 规约](#oop-规约)
- [集合处理](#集合处理)
- [并发处理](#并发处理)
- [控制语句](#控制语句)
- [注释规约](#注释规约)
- [异常处理](#异常处理)
- [MySQL 数据库](#mysql-数据库)

---

## 命名风格

### 基本规则

1. **【强制】** 代码中的命名均不能以下划线或美元符号开始或结束

```java
// 反例
_name / __name / $Object / name_ / name$ / Object$
```

2. **【强制】** 严禁使用拼音与英文混合，更不允许使用中文

3. **【强制】** 类名使用 UpperCamelCase 风格

```java
// 正例
MarcoPolo / UserDO / XmlService / TcpUdpDeal / TaPromotion

// 反例
macroPolo / UserDo / XMLService / TCPUDPDeal / TAPromotion
```

4. **【强制】** 方法名、参数名、成员变量、局部变量使用 lowerCamelCase 风格

```java
// 正例
localValue / getHttpMessage() / inputUserId
```

5. **【强制】** 常量命名全部大写，单词间用下划线隔开

```java
// 正例
MAX_STOCK_COUNT

// 反例
maxCount
```

6. **【强制】** 抽象类使用 Abstract 或 Base 开头；异常类使用 Exception 结尾

7. **【强制】** 类型与中括号紧挨相连表示数组

```java
// 正例
int[] arrayDemo;

// 反例
int arrayDemo[];
```

8. **【强制】** POJO 类布尔变量不加 is 前缀

```java
// 反例
Boolean isDeleted;

// 正例
Boolean deleted;
```

9. **【强制】** 包名统一小写

```java
// 正例
com.alibaba.open.util
```

---

## 常量定义

### 规则

1. **【强制】** 不允许魔法值直接出现在代码中

```java
// 反例
String key = "Id#taobao_" + tradeId;
```

2. **【强制】** long 或 Long 赋值时，数值后使用大写 L

```java
// 正例
Long count = 2L;

// 反例
Long count = 2l;
```

---

## 代码格式

### 规则

1. **【强制】** 大括号内为空，简洁写成 {}

2. **【强制】** 左右小括号和相邻字符间不加空格

3. **【强制】** if/for/while/switch/do 等保留字与括号间加空格

4. **【强制】** 任何二目、三目运算符左右两边加空格

5. **【强制】** 采用 4 个空格缩进

6. **【强制】** 单行字符数不超过 120 个

---

## OOP 规约

### 规则

1. **【强制】** 避免通过对象引用访问静态变量或静态方法

2. **【强制】** 所有覆写方法加 @Override 注解

3. **【强制】** 相同参数类型、相同业务含义才可使用可变参数

4. **【强制】** 外部正在调用的接口，不允许修改方法签名

5. **【强制】** 不能使用过时的类或方法

6. **【强制】** 使用常量或有值的对象调用 equals

```java
// 正例
"test".equals(object);

// 反例
object.equals("test");
```

7. **【强制】** 所有相同类型包装类对象比较使用 equals

8. **【强制】** POJO 类属性使用包装数据类型

---

## 集合处理

### 规则

1. **【强制】** 只要覆写 equals，就必须覆写 hashCode

2. **【强制】** ArrayList 的 subList 不可强转成 ArrayList

3. **【强制】** 使用 Map 的 keySet()/values()/entrySet() 返回集合不可添加元素

4. **【强制】** 使用集合转数组必须用 toArray(T[] array)

---

## 并发处理

### 规则

1. **【强制】** 获取单例对象需要保证线程安全

2. **【强制】** 创建线程或线程池指定有意义的线程名称

3. **【强制】** 线程资源必须通过线程池提供

4. **【强制】** 线程池不允许使用 Executors 创建

```java
// 正例
ThreadPoolExecutor executor = new ThreadPoolExecutor(
    corePoolSize,
    maximumPoolSize,
    keepAliveTime,
    TimeUnit.SECONDS,
    new LinkedBlockingQueue<>()
);

// 反例
ExecutorService executor = Executors.newFixedThreadPool(10);
```

5. **【强制】** SimpleDateFormat 是线程不安全的

---

## 控制语句

### 规则

1. **【强制】** switch 块内每个 case 要么终止，要么注释说明

2. **【强制】** if/else/for/while/do 必须使用大括号

3. **【推荐】** 表达异常分支少用 if-else

---

## 注释规约

### 规则

1. **【强制】** 类、属性、方法注释使用 Javadoc 规范

2. **【强制】** 所有抽象方法必须使用 Javadoc 注释

3. **【强制】** 所有类必须添加创建者和创建日期

4. **【强制】** 方法内部单行注释使用 //

---

## 异常处理

### 规则

1. **【强制】** Java 类库 RuntimeException 不应该通过 catch 处理

2. **【强制】** 异常捕获后不要用来做流程控制

3. **【强制】** 捕获异常是为了处理它，不要捕获后什么都不处理

---

## MySQL 数据库

### 建表规约

1. **【强制】** 布尔字段使用 is_xxx 命名

2. **【强制】** 表名、字段名使用小写字母或数字

3. **【强制】** 表名不使用复数名词

4. **【强制】** 禁用保留字

5. **【强制】** 小数类型使用 decimal

---

## 参考资料

- [Alibaba Java Coding Guidelines (GitHub)](https://github.com/alibaba/p3c)
- [阿里巴巴 Java 开发手册（嵩山版）](https://github.com/alibaba/p3c/blob/master/Java开发手册(嵩山版).pdf)

---

*本文档基于阿里巴巴 Java 开发手册整理*
