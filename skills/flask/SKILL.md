---
name: flask
description: Provides comprehensive guidance for Flask framework including routing, templates, forms, database integration, extensions, and deployment. Use when the user asks about Flask, needs to create Flask applications, implement web routes, or build Python web applications.
license: Apache-2.0
---

## When to use this skill

Use this skill whenever the user wants to:
- 用 Flask 编写 Python Web 应用、路由、模板与扩展
- 配置 WSGI、蓝图、配置与部署

## How to use this skill

1. **核心**：Flask(__name__)、@app.route、request、render_template；Jinja2。
2. **进阶**：Blueprint、Flask-SQLAlchemy、配置与环境变量；g、session。
3. **参考**：https://flask.palletsprojects.com/

## Best Practices

- 应用工厂与蓝图拆分；敏感配置不入库。
- 生产用 Gunicorn/uWSGI；CSRF 与安全头。

## Keywords

flask, Python Web, 路由, 模板

## 能力边界

### ✅ 适用场景
- 当你需要使用此技能对应的技术栈时
- 当项目需要遵循最佳实践时
- 当需要快速上手或深入理解核心概念时

### ⚠️ 需要注意
- 复杂业务逻辑需要结合具体场景调整
- 性能优化需要根据实际数据量评估

### ❌ 不适用场景
- 不相关的技术栈或框架
- 需要完全自定义的特殊场景

## 常见陷阱 (Gotchas)

1. **版本兼容性**：注意框架版本与依赖库的兼容性，不同版本 API 可能有差异
2. **配置文件格式**：配置文件格式错误是最常见的问题，建议使用编辑器的语法检查
3. **环境变量**：确保所有必要的环境变量已正确设置，敏感信息不要硬编码
4. **依赖冲突**：多版本共存时注意依赖冲突，使用 lock 文件锁定版本
5. **性能陷阱**：大数据量场景下注意性能优化，避免 N+1 查询等常见问题

## 使用流程

### Step 1: 环境准备
确保开发环境已安装必要的依赖和工具。

### Step 2: 配置初始化
根据项目需求进行基础配置。

### Step 3: 核心功能使用
按照示例代码实现核心功能。

### Step 4: 测试验证
运行测试确保功能正常。

### Step 5: 部署上线
完成开发后进行部署和监控。
