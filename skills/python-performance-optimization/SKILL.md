---
name: python-performance-optimization
description: Profile and optimize Python code using cProfile, memory profilers, and performance best practices. Use when debugging slow Python code, optimizing bottlenecks, or improving application performance.
---


## 中文描述

本技能提供全栈开发相关的最佳实践和模式指导。

---
name: python-performance-optimization
description: Profile and optimize Python code using cProfile, memory profilers, and performance best practices. Use when debugging slow Python code, optimizing bottlenecks, or improving application performance.
---

# Python Performance Optimization

Comprehensive guide to profiling, analyzing, and optimizing Python code for better performance, including CPU profiling, memory optimization, and implementation best practices.

## When to Use This Skill

- Identifying performance bottlenecks in Python applications
- Reducing application latency and response times
- Optimizing CPU-intensive operations
- Reducing memory consumption and memory leaks
- Improving database query performance
- Optimizing I/O operations
- Speeding up data processing pipelines
- Implementing high-performance algorithms
- Profiling production applications

## Core Concepts

### 1. Profiling Types

- **CPU Profiling**: Identify time-consuming functions
- **Memory Profiling**: Track memory allocation and leaks
- **Line Profiling**: Profile at line-by-line granularity
- **Call Graph**: Visualize function call relationships

### 2. Performance Metrics

- **Execution Time**: How long operations take
- **Memory Usage**: Peak and average memory consumption
- **CPU Utilization**: Processor usage patterns
- **I/O Wait**: Time spent on I/O operations

### 3. Optimization Strategies

- **Algorithmic**: Better algorithms and data structures
- **Implementation**: More efficient code patterns
- **Parallelization**: Multi-threading/processing
- **Caching**: Avoid redundant computation
- **Native Extensions**: C/Rust for critical paths

## Quick Start

### Basic Timing

```python
import time

def measure_time():
    """Simple timing measurement."""
    start = time.time()

    # Your code here
    result = sum(range(1000000))

    elapsed = time.time() - start
    print(f"Execution time: {elapsed:.4f} seconds")
    return result

# Better: use timeit for accurate measurements
import timeit

execution_time = timeit.timeit(
    "sum(range(1000000))",
    number=100
)
print(f"Average time: {execution_time/100:.6f} seconds")
```

## Detailed patterns and worked examples

Detailed pattern documentation lives in `references/details.md`. Read that file when the navigation tier above is insufficient.

## Best Practices

1. **Profile before optimizing** - Measure to find real bottlenecks
2. **Focus on hot paths** - Optimize code that runs most frequently
3. **Use appropriate data structures** - Dict for lookups, set for membership
4. **Avoid premature optimization** - Clarity first, then optimize
5. **Use built-in functions** - They're implemented in C
6. **Cache expensive computations** - Use lru_cache
7. **Batch I/O operations** - Reduce system calls
8. **Use generators** for large datasets
9. **Consider NumPy** for numerical operations
10. **Profile production code** - Use py-spy for live systems

## Common Pitfalls

- Optimizing without profiling
- Using global variables unnecessarily
- Not using appropriate data structures
- Creating unnecessary copies of data
- Not using connection pooling for databases
- Ignoring algorithmic complexity
- Over-optimizing rare code paths
- Not considering memory usage

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
