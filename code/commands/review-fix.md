---
allowed-tools: Bash(git diff:*), Bash(npm run:*), Bash(npx:*), Bash(pytest:*), Bash(go test:*), Read, Edit, Write
description: 修复代码评审中发现的问题，提供可直接应用的修复方案
---

## Context

- Current git status: !`git status`
- Recent changes: !`git diff HEAD --stat`
- Project type: !`[ -f package.json ] && ([ -f vue.config.js ] || [ -f vite.config.js ] || grep -q '"vue"' package.json 2>/dev/null) && echo "Vue" || ([ -f angular.json ] && echo "Angular" || ([ -f next.config.js ] && echo "Next.js" || ([ -f svelte.config.js ] && echo "Svelte" || echo "Node.js")))) || ([ -f go.mod ] && echo "Go" || ([ -f pom.xml ] && echo "Java" || ([ -f pyproject.toml ] || [ -f setup.py ]) && echo "Python" || ([ -f *.csproj ] && echo "CSharp" || ([ -f CMakeLists.txt ] || [ -f Makefile ]) && echo "C/C++" || echo "Unknown")))) 2>/dev/null || echo "Unknown"`

### 当前项目适用规范

!`[ -f package.json ] && ([ -f vue.config.js ] || [ -f vite.config.js ] || grep -q '"vue"' package.json 2>/dev/null) && echo "📖 Vue: [Google-JavaScript-规范.md](../company-coding-standards/Google-JavaScript-规范.md) | [Google-TypeScript-规范.md](../company-coding-standards/Google-TypeScript-规范.md) | [Airbnb-React-规范.md](../company-coding-standards/Airbnb-React-规范.md)" || ([ -f angular.json ] && echo "📖 Angular: [Google-JavaScript-规范.md](../company-coding-standards/Google-JavaScript-规范.md) | [Google-TypeScript-规范.md](../company-coding-standards/Google-TypeScript-规范.md) | [Google-AngularJS-规范.md](../company-coding-standards/Google-AngularJS-规范.md)" || ([ -f next.config.js ] && echo "📖 Next.js/React: [Google-JavaScript-规范.md](../company-coding-standards/Google-JavaScript-规范.md) | [Google-TypeScript-规范.md](../company-coding-standards/Google-TypeScript-规范.md) | [Airbnb-React-规范.md](../company-coding-standards/Airbnb-React-规范.md)" || ([ -f svelte.config.js ] && echo "📖 Svelte: [Google-JavaScript-规范.md](../company-coding-standards/Google-JavaScript-规范.md) | [Google-TypeScript-规范.md](../company-coding-standards/Google-TypeScript-规范.md)" || echo "📖 JavaScript/TypeScript: [Google-JavaScript-规范.md](../company-coding-standards/Google-JavaScript-规范.md) | [Google-TypeScript-规范.md](../company-coding-standards/Google-TypeScript-规范.md)")))) || ([ -f go.mod ] && echo "📖 Go: [Google-Go-规范.md](../company-coding-standards/Google-Go-规范.md) | [Uber-Go-规范.md](../company-coding-standards/Uber-Go-规范.md)" || ([ -f pom.xml ] && echo "📖 Java: [Google-Java-规范.md](../company-coding-standards/Google-Java-规范.md) | [Alibaba-Java-规范.md](../company-coding-standards/Alibaba-Java-规范.md)" || ([ -f pyproject.toml ] || [ -f setup.py ]) && echo "📖 Python: [Google-Python-规范.md](../company-coding-standards/Google-Python-规范.md) | [Python-PEP8-规范.md](../company-coding-standards/Python-PEP8-规范.md)" || ([ -f *.csproj ] && echo "📖 C#: [Google-CSharp-规范.md](../company-coding-standards/Google-CSharp-规范.md)" || ([ -f CMakeLists.txt ] || [ -f Makefile ]) && echo "📖 C/C++: [Google-C++-规范.md](../company-coding-standards/Google-C++-规范.md) | [Linux-C-规范.md](../company-coding-standards/Linux-C-规范.md)" || echo "📖 请手动选择适用的代码规范"))))) 2>/dev/null || echo "📖 请手动选择适用的代码规范"`

## 修复策略总览

| 优先级 | 类别 | 修复难度 | 自动化程度 |
|--------|------|----------|------------|
| 🔴 P0 | 安全漏洞 | 中-高 | 部分自动 |
| 🟠 P1 | 业务逻辑错误 | 高 | 手动 |
| 🟡 P2 | 性能问题 | 中 | 半自动 |
| 🟢 P3 | 代码质量 | 低 | 大部分自动 |
| 🔵 P4 | 可扩展性 | 中-高 | 手动 |

---

## 🔴 安全漏洞修复

### SQL 注入

**问题识别：**
```python
# ❌ 危险：直接拼接 SQL
query = f"SELECT * FROM users WHERE id = {user_input}"

# ❌ 危险：字符串格式化
cursor.execute("SELECT * FROM users WHERE name = '%s'" % name)
```

**修复方案：**
```python
# ✅ 安全：参数化查询
cursor.execute("SELECT * FROM users WHERE id = %s", (user_input,))

# ✅ 安全：ORM 框架
User.objects.filter(id=user_input)

# ✅ 安全：预处理语句 (Go)
stmt, _ := db.Prepare("SELECT * FROM users WHERE id = ?")
rows, _ := stmt.Query(userID)
```

### XSS 跨站脚本攻击

**问题识别：**
```javascript
// ❌ 危险：直接插入 HTML
element.innerHTML = userInput;

// ❌ 危险：React 危险 API（需配合净化器）
// 使用 dangerouslySetInnerHTML 前必须用 DOMPurify 净化
```

**修复方案：**
```javascript
// ✅ 安全：使用 textContent
element.textContent = userInput;

// ✅ 安全：React 默认转义（推荐）
// React 会自动转义 HTML，直接使用即可
<div>{userContent}</div>

// ✅ 安全：必须渲染 HTML 时使用 DOMPurify
import DOMPurify from 'dompurify';
// 先净化再渲染
const cleanHtml = DOMPurify.sanitize(userContent);
```

### 命令注入

**问题识别：**
```python
# ❌ 危险：直接执行用户输入
os.system(f"ping {user_host}")

# ❌ 危险：shell=True
subprocess.run(f"ls {directory}", shell=True)
```

**修复方案：**
```python
# ✅ 安全：使用参数列表
subprocess.run(["ping", user_host], shell=False)

# ✅ 安全：白名单验证
ALLOWED_HOSTS = ['localhost', '127.0.0.1']
if user_host in ALLOWED_HOSTS:
    subprocess.run(["ping", user_host])
```

### 敏感信息泄露

**问题识别：**
```javascript
// ❌ 危险：硬编码密钥
const API_KEY = "sk-xxxxx";

// ❌ 危险：日志输出敏感信息
console.log("User login:", password);
```

**修复方案：**
```javascript
// ✅ 安全：环境变量
const API_KEY = process.env.API_KEY;

// ✅ 安全：配置文件（gitignore）
import config from './config.local.json';

// ✅ 安全：日志脱敏
logger.info("User login:", { username: user.name, password: "***" });
```

---

## 🟠 业务逻辑错误修复

### 竞态条件

**问题识别：**
```python
# ❌ 问题：检查和操作分离
if account.balance >= amount:
    account.balance -= amount  # 并发时可能出错
```

**修复方案：**
```python
# ✅ 正确：使用数据库事务
with transaction.atomic():
    account = Account.objects.select_for_update().get(id=account_id)
    if account.balance >= amount:
        account.balance -= amount
        account.save()

# ✅ 正确：乐观锁
UPDATE accounts SET balance = balance - ?
WHERE id = ? AND balance >= ?
```

### 边界条件错误

**问题识别：**
```javascript
// ❌ 问题：未处理边界
function getPage(items, page, size) {
    return items.slice(page * size, (page + 1) * size);
}
```

**修复方案：**
```javascript
// ✅ 正确：边界验证
function getPage(items, page, size) {
    const pageSize = Math.max(1, Math.min(size, 100)); // 限制 1-100
    const pageNum = Math.max(0, page); // 非负数
    const start = pageNum * pageSize;
    const end = Math.min(start + pageSize, items.length);
    return items.slice(start, end);
}
```

### 空值/未定义处理

**问题识别：**
```javascript
// ❌ 问题：链式调用可能报错
const name = user.profile.settings.name;

// ❌ 问题：未处理 null
function process(data) {
    return data.map(item => item.value);
}
```

**修复方案：**
```javascript
// ✅ 正确：可选链 + 空值合并
const name = user?.profile?.settings?.name ?? 'Unknown';

// ✅ 正确：防御性编程
function process(data) {
    if (!Array.isArray(data)) return [];
    return data.filter(Boolean).map(item => item?.value);
}
```

---

## 🟡 性能问题修复

### N+1 查询问题

**问题识别：**
```python
# ❌ 问题：循环中查询数据库
for order in orders:
    user = User.objects.get(id=order.user_id)  # N 次查询
    print(user.name)
```

**修复方案：**
```python
# ✅ 优化：预加载关联数据
orders = Order.objects.select_related('user').all()
for order in orders:
    print(order.user.name)  # 只需 1-2 次查询

# ✅ 优化：批量查询 + 缓存
user_ids = [o.user_id for o in orders]
users = {u.id: u for u in User.objects.filter(id__in=user_ids)}
for order in orders:
    print(users[order.user_id].name)
```

**JavaScript/TypeScript:**
```typescript
// ❌ 问题
for (const post of posts) {
    const author = await db.users.findUnique({ where: { id: post.authorId } });
}

// ✅ 优化：批量查询
const authorIds = [...new Set(posts.map(p => p.authorId))];
const authors = await db.users.findMany({ where: { id: { in: authorIds } } });
const authorMap = new Map(authors.map(a => [a.id, a]));
```

### 缺失索引

**问题识别：**
```sql
-- 慢查询：无索引的全表扫描
SELECT * FROM orders WHERE user_id = 123 AND created_at > '2024-01-01';
```

**修复方案：**
```sql
-- ✅ 添加复合索引
CREATE INDEX idx_orders_user_created ON orders(user_id, created_at);

-- ✅ 分析执行计划确认
EXPLAIN ANALYZE SELECT * FROM orders WHERE user_id = 123 AND created_at > '2024-01-01';
```

### 内存泄漏

**问题识别：**
```javascript
// ❌ 问题：未清理的事件监听器
useEffect(() => {
    window.addEventListener('resize', handleResize);
}, []); // 缺少 cleanup
```

**修复方案：**
```javascript
// ✅ 正确：清理副作用
useEffect(() => {
    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
}, []);
```

### 低效循环

**问题识别：**
```javascript
// ❌ 问题：嵌套循环 O(n²)
for (const user of users) {
    for (const order of orders) {
        if (order.userId === user.id) {
            user.orders.push(order);
        }
    }
}
```

**修复方案：**
```javascript
// ✅ 优化：使用 Map O(n)
const orderMap = new Map();
for (const order of orders) {
    if (!orderMap.has(order.userId)) orderMap.set(order.userId, []);
    orderMap.get(order.userId).push(order);
}
for (const user of users) {
    user.orders = orderMap.get(user.id) || [];
}
```

---

## 🟢 代码质量修复

### 代码规范参考

> 规范文件位于 `company-coding-standards/` 目录

| 语言 | 规范文件 | 官方文档 |
|------|----------|----------|
| Python | [Google-Python-规范.md](../company-coding-standards/Google-Python-规范.md) | https://google.github.io/styleguide/pyguide.html |
| JavaScript | [Google-JavaScript-规范.md](../company-coding-standards/Google-JavaScript-规范.md) | https://google.github.io/styleguide/jsguide.html |
| TypeScript | [Google-TypeScript-规范.md](../company-coding-standards/Google-TypeScript-规范.md) | https://google.github.io/styleguide/tsguide.html |
| Go | [Google-Go-规范.md](../company-coding-standards/Google-Go-规范.md) | https://google.github.io/styleguide/go/ |
| Java | [Google-Java-规范.md](../company-coding-standards/Google-Java-规范.md) | https://google.github.io/styleguide/javaguide.html |
| C++ | [Google-C++-规范.md](../company-coding-standards/Google-C++-规范.md) | https://google.github.io/styleguide/cppguide.html |
| C# | [Google-CSharp-规范.md](../company-coding-standards/Google-CSharp-规范.md) | https://google.github.io/styleguide/csharp-style.html |
| Shell | [Google-Shell-规范.md](../company-coding-standards/Google-Shell-规范.md) | https://google.github.io/styleguide/shellguide.html |
| HTML/CSS | [Google-HTML-CSS-规范.md](../company-coding-standards/Google-HTML-CSS-规范.md) | https://google.github.io/styleguide/htmlcssguide.html |

**其他规范：**
- [Alibaba-Java-规范.md](../company-coding-standards/Alibaba-Java-规范.md)
- [Airbnb-JavaScript-规范.md](../company-coding-standards/Airbnb-JavaScript-规范.md)
- [Airbnb-React-规范.md](../company-coding-standards/Airbnb-React-规范.md)
- [Uber-Go-规范.md](../company-coding-standards/Uber-Go-规范.md)
- [Python-PEP8-规范.md](../company-coding-standards/Python-PEP8-规范.md)
- [Microsoft-TypeScript-规范.md](../company-coding-standards/Microsoft-TypeScript-规范.md)

### 自动修复命令

```bash
# JavaScript/TypeScript
npx eslint --fix .
npx prettier --write .

# Python
black .
isort .
autoflake --remove-all-unused-imports --in-place -r .

# Go
go fmt ./...
goimports -w .
```

### 命名规范

| 问题 | ❌ 不好的命名 | ✅ 好的命名 |
|------|---------------|-------------|
| 无意义变量 | `d, temp, data` | `userData, tempDirectory` |
| 布尔值 | `flag, status` | `isValid, hasPermission` |
| 函数 | `process(), handle()` | `processPayment(), handleUserLogin()` |
| 常量 | `magic numbers` | `MAX_RETRY_COUNT = 3` |

### 重复代码抽取

**问题识别：**
```javascript
// ❌ 重复代码
function validateEmail(email) {
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return regex.test(email);
}
function validateUserEmail(email) {
    const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return regex.test(email);
}
```

**修复方案：**
```javascript
// ✅ 抽取公共函数
const EMAIL_REGEX = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

function isValidEmail(email) {
    return EMAIL_REGEX.test(email);
}

// 使用
function validateUser(user) {
    return isValidEmail(user.email);
}
```

### 函数过长拆分

**原则：**
- 单一职责：一个函数只做一件事
- 长度限制：一般不超过 50 行
- 参数数量：不超过 3-4 个

```javascript
// ❌ 过长函数
async function processOrder(order) {
    // 验证逻辑 20 行
    // 计算价格 30 行
    // 更新库存 20 行
    // 发送通知 15 行
    // 记录日志 10 行
}

// ✅ 拆分后
async function processOrder(order) {
    validateOrder(order);
    const total = calculateTotal(order);
    await updateInventory(order.items);
    await sendConfirmation(order, total);
    logOrder(order, total);
}
```

---

## 🔵 可扩展性修复

### 硬编码配置

**问题识别：**
```javascript
// ❌ 硬编码
const MAX_ITEMS = 100;
const API_URL = "https://api.example.com";
const TIMEOUT = 30000;
```

**修复方案：**
```javascript
// ✅ 配置化
const config = {
    maxItems: parseInt(process.env.MAX_ITEMS) || 100,
    apiUrl: process.env.API_URL || 'https://api.example.com',
    timeout: parseInt(process.env.TIMEOUT) || 30000,
};
```

### 紧耦合

**问题识别：**
```python
# ❌ 紧耦合：直接依赖具体实现
class OrderService:
    def __init__(self):
        self.stripe = StripePaymentGateway()

    def pay(self, order):
        return self.stripe.charge(order.total)
```

**修复方案：**
```python
# ✅ 依赖注入：面向接口编程
class OrderService:
    def __init__(self, payment_gateway: PaymentGateway):
        self.payment_gateway = payment_gateway

    def pay(self, order):
        return self.payment_gateway.charge(order.total)

# 使用
service = OrderService(StripePaymentGateway())
# 或
service = OrderService(PayPalPaymentGateway())
```

### 缺乏抽象

**问题识别：**
```javascript
// ❌ 缺乏抽象：到处重复的 API 调用
async function getUser(id) {
    const response = await fetch(`/api/users/${id}`);
    if (!response.ok) throw new Error('Failed');
    return response.json();
}
async function getPost(id) {
    const response = await fetch(`/api/posts/${id}`);
    if (!response.ok) throw new Error('Failed');
    return response.json();
}
```

**修复方案：**
```javascript
// ✅ 抽象基础方法
async function apiRequest(endpoint, options = {}) {
    const response = await fetch(`/api${endpoint}`, {
        headers: { 'Content-Type': 'application/json' },
        ...options,
    });
    if (!response.ok) {
        throw new ApiError(response.status, await response.text());
    }
    return response.json();
}

// 使用
const getUser = (id) => apiRequest(`/users/${id}`);
const getPost = (id) => apiRequest(`/posts/${id}`);
```

---

## Your task

Based on code review feedback:

1. **分析问题** - 确定问题类型和优先级
2. **自动修复** - 运行 linter 的 --fix 选项
3. **手动修复** - 根据上述指南提供具体修复方案：
   - 展示问题代码
   - 解释问题原因
   - 提供修复后的代码
   - 说明修复原理
4. **验证修复** - 运行测试和 linter 确认

### 输出格式

```markdown
## 修复报告

### 🔴 安全漏洞 (P0)
| 文件 | 行号 | 问题 | 修复状态 |
|------|------|------|----------|
| xxx  | 42   | SQL注入 | ✅ 已修复 |

### 🟡 性能问题 (P2)
...

### 总结
- 自动修复: X 个
- 手动修复: Y 个
- 需关注: Z 个
```
