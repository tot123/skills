---
description: 修复代码评审问题
tags: [fix, refactor, review]
---

# code-review-fix

修复代码评审中发现的问题。

## 功能

1. **分析评审意见** - 理解需要修复的问题
2. **自动修复** - 修复可以自动处理的问题
3. **辅助修复** - 为复杂问题提供修复指导
4. **验证修复** - 确保修复正确且不引入新问题

## 问题分类

### 自动可修复

| 类型 | 修复方式 |
|------|----------|
| 代码格式 | 使用 prettier/eslint --fix |
| 命名规范 | 自动重命名（IDE 支持） |
| 未使用导入 | 自动删除 |
| 简单类型错误 | 添加类型注解 |
| 文档缺失 | 生成文档模板 |

### 需要手动修复

| 类型 | 处理方式 |
|------|----------|
| 逻辑错误 | 分析并重写逻辑 |
| 安全漏洞 | 评估并实施安全修复 |
| 性能问题 | 分析瓶颈并优化 |
| 架构问题 | 重构代码结构 |
| 复杂重构 | 逐步修改并测试 |

## 修复流程

```
1. 接收评审意见
       ↓
2. 分类问题（自动/手动）
       ↓
3. 自动修复可处理的问题
       ↓
4. 逐个处理手动问题
       ↓
5. 运行测试验证
       ↓
6. 提交修复
```

## 常见问题修复指南

### 1. 安全漏洞修复

#### SQL 注入

```python
# 不安全：直接拼接
cursor.execute(f"SELECT * FROM users WHERE id = {user_id}")

# 安全：参数化查询
cursor.execute("SELECT * FROM users WHERE id = ?", (user_id,))
```

#### XSS 攻击防护

```typescript
// 危险：直接设置 HTML
// element.innerHTML = userInput;  // 不要这样做

// 安全方式 1：使用 textContent
element.textContent = userInput;

// 安全方式 2：使用 HTML 净化库（如 DOMPurify）
// element.innerHTML = DOMPurify.sanitize(userInput);
```

### 2. 性能优化

#### 循环优化

```javascript
// 低效：每次循环都访问 length
for (let i = 0; i < array.length; i++) {
    process(array[i]);
}

// 高效：缓存 length
const len = array.length;
for (let i = 0; i < len; i++) {
    process(array[i]);
}
```

#### 查找优化

```typescript
// 低效：O(n) 查找
const found = users.find(u => u.id === targetId);

// 高效：O(1) 查找
const userMap = new Map(users.map(u => [u.id, u]));
const found = userMap.get(targetId);
```

### 3. 错误处理

```typescript
// 不当：吞掉错误
try {
    doSomething();
} catch (e) {
    // 什么都不做 - 这是错误的做法
}

// 正确：记录并处理错误
try {
    doSomething();
} catch (e) {
    logger.error('Failed to do something', e);
    throw new ApplicationError('Operation failed', e);
}
```

### 4. 代码重复

```typescript
// 问题：重复代码
function validateEmail(email: string) {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}
function validateUserEmail(email: string) {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
}

// 解决：提取公共逻辑
const EMAIL_REGEX = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
function validateEmail(email: string): boolean {
    return EMAIL_REGEX.test(email);
}
```

## 执行步骤

当用户调用此命令时：

1. 获取最近的评审意见（或接收用户输入）
2. 分析问题类型和严重程度
3. 对于可自动修复的问题：
   - 执行自动修复命令
   - 显示修复结果
4. 对于需手动修复的问题：
   - 提供修复建议和示例代码
   - 指导用户完成修复
5. 运行相关测试验证修复
6. 生成修复报告

## 修复报告格式

```markdown
## 修复报告

### 自动修复
- [x] 格式化代码 (3 个文件)
- [x] 删除未使用导入 (5 处)
- [x] 修复命名规范 (2 处)

### 手动修复指导

#### 问题 1: SQL 注入漏洞
- 文件: `src/db/queries.py:42`
- 修复方式: 使用参数化查询
- 示例代码已提供

#### 问题 2: 缺少错误处理
- 文件: `src/api/handlers.ts:88`
- 修复方式: 添加 try-catch 和日志
- 示例代码已提供

### 验证结果
- 单元测试: 通过
- Lint 检查: 通过
- 类型检查: 通过
```

## 最佳实践

1. **一次修复一个问题** - 避免引入新 bug
2. **保持小范围** - 不要扩大修改范围
3. **添加测试** - 为修复添加测试用例
4. **更新文档** - 如有需要更新相关文档
5. **提交信息** - 说明修复了什么问题

## 参考资源

- [Google Engineering Practices - Handling Comments](https://google.github.io/eng-practices/review/developer/handling-comments.html)
- [How to do a Code Review](https://google.github.io/eng-practices/review/reviewer/)
