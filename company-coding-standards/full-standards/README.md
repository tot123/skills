# 全球代码规范完整汇总

> 收集整理了全球知名科技公司的代码规范，包括国际大厂和国内大厂

---

## 📊 统计总览

| 分类 | 公司数量 | 规范文件数 |
|------|----------|------------|
| 国际大厂 | 7 | 50+ |
| 国内大厂 | 5 | 20+ |
| **总计** | **12** | **69** |

---

## 📁 目录结构

```
full-standards/
├── Google/                    # Google 代码规范 (17 种语言) - 全部 Markdown 格式
├── Airbnb/                    # Airbnb 代码规范
├── Alibaba/                   # 阿里巴巴 Java 开发手册
├── Uber/                      # Uber 代码规范
├── Twitter/                   # Twitter 代码规范
├── Others/                    # 其他规范汇总
└── China/                     # 国内大厂规范
    ├── Tencent/               # 腾讯安全规范
    ├── Baidu/                 # 百度前端规范
    ├── 360/                   # 360 C/C++ 安全规范
    ├── Xiaomi/                # 小米贡献指南
    └── Collection/            # 规范汇总
```

---

## 🌍 国际大厂

### Google（17 种语言）- 全部 Markdown 格式

| 语言 | 文件 | 官方链接 |
|------|------|----------|
| C++ | cppguide.md | [官方文档](https://google.github.io/styleguide/cppguide.html) |
| Java | javaguide.md | [官方文档](https://google.github.io/styleguide/javaguide.html) |
| Python | pyguide.md | [官方文档](https://google.github.io/styleguide/pyguide.html) |
| JavaScript | jsguide.md | [官方文档](https://google.github.io/styleguide/jsguide.html) |
| TypeScript | tsguide.md | [官方文档](https://google.github.io/styleguide/tsguide.html) |
| Go | go/guide.md | [官方文档](https://google.github.io/styleguide/go/) |
| C# | csharp-style.md | [官方文档](https://google.github.io/styleguide/csharp-style.html) |
| Objective-C | objcguide.md | [官方文档](https://google.github.io/styleguide/objcguide.html) |
| Shell | shellguide.md | [官方文档](https://google.github.io/styleguide/shellguide.html) |
| R | Rguide.md | [官方文档](https://google.github.io/styleguide/Rguide.html) |
| HTML/CSS | htmlcssguide.md | [官方文档](https://google.github.io/styleguide/htmlcssguide.html) |
| JSON | jsoncstyleguide.md | [官方文档](https://google.github.io/styleguide/jsoncstyleguide.html) |
| Markdown | markdown-style.md | [官方文档](https://google.github.io/styleguide/docguide/style.html) |
| AngularJS | angularjs-google-style.md | [官方文档](https://google.github.io/styleguide/angularjs-google-style.html) |
| Common Lisp | lispguide.xml | [官方文档](https://google.github.io/styleguide/lispguide.html) |
| Vim script | vimscriptguide.xml | [官方文档](https://google.github.io/styleguide/vimscriptguide.xml) |

### Airbnb

| 语言 | 文件 | 链接 |
|------|------|------|
| JavaScript | javascript.md | [GitHub](https://github.com/airbnb/javascript) |
| React | react/README.md | [GitHub](https://github.com/airbnb/javascript/tree/master/react) |
| CSS-in-JS | css-in-javascript/README.md | [GitHub](https://github.com/airbnb/javascript/tree/master/css-in-javascript) |

### Alibaba

| 语言 | 内容 | 链接 |
|------|------|------|
| Java | 完整开发手册 | [GitHub](https://github.com/alibaba/p3c) |
| MySQL | 数据库规范 | 内含 |
| 工程结构 | 项目架构规范 | 内含 |

### Uber

| 语言 | 文件 | 链接 |
|------|------|------|
| Go | go-style.md | [GitHub](https://github.com/uber-go/guide) |

### Twitter

| 语言 | 文件 | 链接 |
|------|------|------|
| Scala | effectivescala.mo (多语言) | [GitHub](https://github.com/twitter/effectivescala) |

---

## 🇨🇳 国内大厂

### 腾讯 Tencent

| 规范 | 文件 | 说明 |
|------|------|------|
| C/C++ 安全 | C,C++安全指南.md | 安全编码规范 |
| Java 安全 | Java安全指南.md | Java 安全规范 |
| Python 安全 | Python安全指南.md | Python 安全规范 |
| JavaScript 安全 | JavaScript安全指南.md | JS 安全规范 |
| Go 安全 | Go安全指南.md | Go 安全规范 |

**GitHub**: [tencent/secguide](https://github.com/tencent/secguide)

### 百度 Baidu

| 规范 | 文件 | 说明 |
|------|------|------|
| HTML | html.md | HTML 编码规范 |
| CSS | css.md | CSS 编码规范 |
| JavaScript | javascript.md | JS 编码规范 |
| Markdown | markdown.md | Markdown 规范 |
| EditorConfig | editorconfig.md | 编辑器配置 |
| 安全 | security.md | 安全规范 |
| 项目 | project.md | 项目规范 |

**GitHub**: [fex-team/styleguide](https://github.com/fex-team/styleguide)

### 360

| 规范 | 文件 | 说明 |
|------|------|------|
| C/C++ 规则 | c-cpp-rules.md | C/C++ 编程规范 |
| C 未定义行为 | c-ub-list.md | C 语言 UB 列表 |
| C++ 未定义行为 | cpp-ub-list.md | C++ 语言 UB 列表 |

**GitHub**: [Qihoo360/safe-rules](https://github.com/Qihoo360/safe-rules)

### 小米 Xiaomi

| 规范 | 文件 | 说明 |
|------|------|------|
| MACE 贡献指南 | mace-contributing.md | 包含 Python/C++ 编码规范 |

**GitHub**: [XiaoMi/mace](https://github.com/XiaoMi/mace)

---

## 📥 原始仓库列表

### 国际大厂

| 公司 | 仓库 | 大小 |
|------|------|------|
| Google | [google/styleguide](https://github.com/google/styleguide) | 3.7 MB |
| Google 中文 | [zh-google-styleguide](https://github.com/zh-google-styleguide/zh-google-styleguide) | 1.2 MB |
| Airbnb | [airbnb/javascript](https://github.com/airbnb/javascript) | 686 KB |
| Alibaba | [alibaba/p3c](https://github.com/alibaba/p3c) | 9.0 MB |
| Uber | [uber-go/guide](https://github.com/uber-go/guide) | 523 KB |
| Twitter | [twitter/effectivescala](https://github.com/twitter/effectivescala) | 606 KB |
| Awesome | [Kristories/awesome-guidelines](https://github.com/Kristories/awesome-guidelines) | 435 KB |

### 国内大厂

| 公司 | 仓库 | 大小 |
|------|------|------|
| 腾讯 | [tencent/secguide](https://github.com/tencent/secguide) | 353 KB |
| 百度 | [fex-team/styleguide](https://github.com/fex-team/styleguide) | 312 KB |
| 360 | [Qihoo360/safe-rules](https://github.com/Qihoo360/safe-rules) | 1.5 MB |
| 小米 | [XiaoMi/mace](https://github.com/XiaoMi/mace) | 63 MB |
| 汇总 | [wangqianfront/coding-styleguide](https://github.com/wangqianfront/coding-styleguide) | 1.9 MB |

---

## 🔗 其他资源

### 国内大厂（非 GitHub）

| 公司 | 资源 | 链接 |
|------|------|------|
| 网易 | NEC 前端规范 | http://nec.netease.com/standard |
| 美团 | 技术博客 | https://tech.meituan.com |
| 字节跳动 | 遵循 Google 规范 | - |
| 京东 | JDC 前端规范 | https://jdf2e.github.io/jdc_fe_guide/ |
| 京东 | 凹凸实验室 | https://guide.aotu.io/ |

---

## 📋 文件格式说明

| 格式 | 数量 | 说明 |
|------|------|------|
| Markdown (.md) | 65 | 主要格式，易于阅读和编辑 |
| XML (.xml) | 2 | Lisp 和 Vim script 规范 |
| 其他 | 2 | 配置文件等 |

---

*最后更新: 2025年3月*
