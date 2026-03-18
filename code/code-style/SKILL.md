---
description: 代码风格与质量检查
tags: [lint, style, quality]
---

# code-style

代码风格与质量检查，确保代码符合团队规范。

## 功能

1. **静态代码分析** - 检测潜在问题
2. **风格一致性检查** - 确保代码风格统一
3. **质量评估** - 评估代码质量指标

## 支持的检查工具

### 多语言支持

| 语言 | 工具 |
|------|------|
| JavaScript/TypeScript | ESLint, Prettier |
| Python | pylint, black, flake8 |
| Go | golint, gofmt |
| Java | Checkstyle, SpotBugs |
| C/C++ | clang-tidy, cpplint |
| Shell | ShellCheck |
| Rust | clippy, rustfmt |

## Google 代码风格指南

### 通用原则

1. **可读性优先** - 代码是写给人看的
2. **一致性** - 遵循项目既定风格
3. **简洁性** - 避免不必要的复杂性
4. **自解释** - 好的命名胜过注释

### 命名规范

```python
# Python 示例
class MyClass:           # 类名：PascalCase
    def my_method(self): # 方法名：snake_case
        my_variable = 1  # 变量名：snake_case
        MY_CONSTANT = 1  # 常量：UPPER_SNAKE_CASE
```

```typescript
// TypeScript 示例
class MyClass {           // 类名：PascalCase
    myMethod(): void {}   // 方法名：camelCase
    private myField;      // 字段名：camelCase
    static readonly MY_CONSTANT = 1; // 常量：UPPER_SNAKE_CASE
}
```

### 代码格式

- 使用 2 或 4 空格缩进（根据语言规范）
- 行长度不超过 80-120 字符
- 使用一致的括号风格
- 合理使用空行分隔逻辑块

## 执行步骤

当用户调用此命令时：

1. 识别项目使用的编程语言
2. 检查是否存在配置文件（.eslintrc, .pylintrc 等）
3. 运行相应的 lint 工具
4. 汇总检查结果
5. 提供修复建议

## 常见问题修复

| 问题 | 修复方式 |
|------|----------|
| 未使用变量 | 删除或使用该变量 |
| 命名不规范 | 重命名以符合规范 |
| 代码过长 | 拆分为更小的函数 |
| 缺少文档 | 添加必要的注释 |

## 参考资源

- [Google Style Guides](https://google.github.io/styleguide/)
- [Google Python Style Guide](https://google.github.io/styleguide/pyguide.html)
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [Google TypeScript Style Guide](https://google.github.io/styleguide/tsguide.html)
