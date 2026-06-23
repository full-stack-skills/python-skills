---
name: python-packaging
description: Create distributable Python packages with proper project structure, setup.py/pyproject.toml, and publishing to PyPI. Use when packaging Python libraries, creating CLI tools, or distributing Python code.
---


## 中文描述

本技能提供全栈开发相关的最佳实践和模式指导。

---
name: python-packaging
description: Create distributable Python packages with proper project structure, setup.py/pyproject.toml, and publishing to PyPI. Use when packaging Python libraries, creating CLI tools, or distributing Python code.
---

# Python Packaging

Comprehensive guide to creating, structuring, and distributing Python packages using modern packaging tools, pyproject.toml, and publishing to PyPI.

## When to Use This Skill

- Creating Python libraries for distribution
- Building command-line tools with entry points
- Publishing packages to PyPI or private repositories
- Setting up Python project structure
- Creating installable packages with dependencies
- Building wheels and source distributions
- Versioning and releasing Python packages
- Creating namespace packages
- Implementing package metadata and classifiers

## Core Concepts

### 1. Package Structure

- **Source layout**: `src/package_name/` (recommended)
- **Flat layout**: `package_name/` (simpler but less flexible)
- **Package metadata**: pyproject.toml, setup.py, or setup.cfg
- **Distribution formats**: wheel (.whl) and source distribution (.tar.gz)

### 2. Modern Packaging Standards

- **PEP 517/518**: Build system requirements
- **PEP 621**: Metadata in pyproject.toml
- **PEP 660**: Editable installs
- **pyproject.toml**: Single source of configuration

### 3. Build Backends

- **setuptools**: Traditional, widely used
- **hatchling**: Modern, opinionated
- **flit**: Lightweight, for pure Python
- **poetry**: Dependency management + packaging

### 4. Distribution

- **PyPI**: Python Package Index (public)
- **TestPyPI**: Testing before production
- **Private repositories**: JFrog, AWS CodeArtifact, etc.

## Quick Start

### Minimal Package Structure

```
my-package/
├── pyproject.toml
├── README.md
├── LICENSE
├── src/
│   └── my_package/
│       ├── __init__.py
│       └── module.py
└── tests/
    └── test_module.py
```

### Minimal pyproject.toml

```toml
[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "my-package"
version = "0.1.0"
description = "A short description"
authors = [{name = "Your Name", email = "you@example.com"}]
readme = "README.md"
requires-python = ">=3.8"
dependencies = [
    "requests>=2.28.0",
]

[project.optional-dependencies]
dev = [
    "pytest>=7.0",
    "black>=22.0",
]
```

## Package Structure Patterns

### Pattern 1: Source Layout (Recommended)

```
my-package/
├── pyproject.toml
├── README.md
├── LICENSE
├── .gitignore
├── src/
│   └── my_package/
│       ├── __init__.py
│       ├── core.py
│       ├── utils.py
│       └── py.typed          # For type hints
├── tests/
│   ├── __init__.py
│   ├── test_core.py
│   └── test_utils.py
└── docs/
    └── index.md
```

**Advantages:**

- Prevents accidentally importing from source
- Cleaner test imports
- Better isolation

**pyproject.toml for source layout:**

```toml
[tool.setuptools.packages.find]
where = ["src"]
```

### Pattern 2: Flat Layout

```
my-package/
├── pyproject.toml
├── README.md
├── my_package/
│   ├── __init__.py
│   └── module.py
└── tests/
    └── test_module.py
```

**Simpler but:**

- Can import package without installing
- Less professional for libraries

### Pattern 3: Multi-Package Project

```
project/
├── pyproject.toml
├── packages/
│   ├── package-a/
│   │   └── src/
│   │       └── package_a/
│   └── package-b/
│       └── src/
│           └── package_b/
└── tests/
```

## Detailed patterns and worked examples

Detailed pattern documentation lives in `references/details.md`. Read that file when the navigation tier above is insufficient.


## 能力边界

### ✅ 擅长处理
- 全栈开发相关的最佳实践
- 代码架构设计指导
- 性能优化建议

### ⚠️ 需要素材
- 具体的项目上下文
- 技术栈信息

### ❌ 超出范围
- 非技术领域的业务决策
- 具体的代码实现（仅提供指导）

## 工作流程

### Step 1: 需求分析
理解项目需求和技术约束

### Step 2: 架构设计
设计系统架构和组件划分

### Step 3: 实现指导
提供具体的实现建议和代码模式

### Step 4: 代码审查
审查代码质量和最佳实践遵循情况

### Step 5: 优化建议
提供性能优化和改进建议

## Gotchas

### 1. 过度设计
避免在简单场景中使用复杂的设计模式

### 2. 性能忽视
不要忽视性能优化，特别是在生产环境中

### 3. 安全考虑
始终考虑安全性和数据保护

### 4. 测试覆盖
确保有足够的测试覆盖，特别是边界情况

### 5. 文档维护
保持文档与代码同步更新
