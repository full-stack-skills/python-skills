---
name: python-resilience
description: Python resilience patterns including automatic retries, exponential backoff, timeouts, and fault-tolerant decorators. Use when adding retry logic, implementing timeouts, building fault-tolerant services, or handling transient failures.
---


## 中文描述

本技能提供全栈开发相关的最佳实践和模式指导。

---
name: python-resilience
description: Python resilience patterns including automatic retries, exponential backoff, timeouts, and fault-tolerant decorators. Use when adding retry logic, implementing timeouts, building fault-tolerant services, or handling transient failures.
---

# Python Resilience Patterns

Build fault-tolerant Python applications that gracefully handle transient failures, network issues, and service outages. Resilience patterns keep systems running when dependencies are unreliable.

## When to Use This Skill

- Adding retry logic to external service calls
- Implementing timeouts for network operations
- Building fault-tolerant microservices
- Handling rate limiting and backpressure
- Creating infrastructure decorators
- Designing circuit breakers

## Core Concepts

### 1. Transient vs Permanent Failures

Retry transient errors (network timeouts, temporary service issues). Don't retry permanent errors (invalid credentials, bad requests).

### 2. Exponential Backoff

Increase wait time between retries to avoid overwhelming recovering services.

### 3. Jitter

Add randomness to backoff to prevent thundering herd when many clients retry simultaneously.

### 4. Bounded Retries

Cap both attempt count and total duration to prevent infinite retry loops.

## Quick Start

```python
from tenacity import retry, stop_after_attempt, wait_exponential_jitter

@retry(
    stop=stop_after_attempt(3),
    wait=wait_exponential_jitter(initial=1, max=10),
)
def call_external_service(request: dict) -> dict:
    return httpx.post("https://api.example.com", json=request).json()
```

## Fundamental Patterns

### Pattern 1: Basic Retry with Tenacity

Use the `tenacity` library for production-grade retry logic. For simpler cases, consider built-in retry functionality or a lightweight custom implementation.

```python
from tenacity import (
    retry,
    stop_after_attempt,
    stop_after_delay,
    wait_exponential_jitter,
    retry_if_exception_type,
)

TRANSIENT_ERRORS = (ConnectionError, TimeoutError, OSError)

@retry(
    retry=retry_if_exception_type(TRANSIENT_ERRORS),
    stop=stop_after_attempt(5) | stop_after_delay(60),
    wait=wait_exponential_jitter(initial=1, max=30),
)
def fetch_data(url: str) -> dict:
    """Fetch data with automatic retry on transient failures."""
    response = httpx.get(url, timeout=30)
    response.raise_for_status()
    return response.json()
```

### Pattern 2: Retry Only Appropriate Errors

Whitelist specific transient exceptions. Never retry:

- `ValueError`, `TypeError` - These are bugs, not transient issues
- `AuthenticationError` - Invalid credentials won't become valid
- HTTP 4xx errors (except 429) - Client errors are permanent

```python
from tenacity import retry, retry_if_exception_type
import httpx

# Define what's retryable
RETRYABLE_EXCEPTIONS = (
    ConnectionError,
    TimeoutError,
    httpx.ConnectTimeout,
    httpx.ReadTimeout,
)

@retry(
    retry=retry_if_exception_type(RETRYABLE_EXCEPTIONS),
    stop=stop_after_attempt(3),
    wait=wait_exponential_jitter(initial=1, max=10),
)
def resilient_api_call(endpoint: str) -> dict:
    """Make API call with retry on network issues."""
    return httpx.get(endpoint, timeout=10).json()
```

### Pattern 3: HTTP Status Code Retries

Retry specific HTTP status codes that indicate transient issues.

```python
from tenacity import retry, retry_if_result, stop_after_attempt
import httpx

RETRY_STATUS_CODES = {429, 502, 503, 504}

def should_retry_response(response: httpx.Response) -> bool:
    """Check if response indicates a retryable error."""
    return response.status_code in RETRY_STATUS_CODES

@retry(
    retry=retry_if_result(should_retry_response),
    stop=stop_after_attempt(3),
    wait=wait_exponential_jitter(initial=1, max=10),
)
def http_request(method: str, url: str, **kwargs) -> httpx.Response:
    """Make HTTP request with retry on transient status codes."""
    return httpx.request(method, url, timeout=30, **kwargs)
```

### Pattern 4: Combined Exception and Status Retry

Handle both network exceptions and HTTP status codes.

```python
from tenacity import (
    retry,
    retry_if_exception_type,
    retry_if_result,
    stop_after_attempt,
    wait_exponential_jitter,
    before_sleep_log,
)
import logging
import httpx

logger = logging.getLogger(__name__)

TRANSIENT_EXCEPTIONS = (
    ConnectionError,
    TimeoutError,
    httpx.ConnectError,
    httpx.ReadTimeout,
)
RETRY_STATUS_CODES = {429, 500, 502, 503, 504}

def is_retryable_response(response: httpx.Response) -> bool:
    return response.status_code in RETRY_STATUS_CODES

@retry(
    retry=(
        retry_if_exception_type(TRANSIENT_EXCEPTIONS) |
        retry_if_result(is_retryable_response)
    ),
    stop=stop_after_attempt(5),
    wait=wait_exponential_jitter(initial=1, max=30),
    before_sleep=before_sleep_log(logger, logging.WARNING),
)
def robust_http_call(
    method: str,
    url: str,
    **kwargs,
) -> httpx.Response:
    """HTTP call with comprehensive retry handling."""
    return httpx.request(method, url, timeout=30, **kwargs)
```

## Detailed worked examples and patterns

Detailed sections (starting with `## Advanced Patterns`) live in `references/details.md`. Read that file when the navigation summary above is insufficient.

## Best Practices Summary

1. **Retry only transient errors** - Don't retry bugs or authentication failures
2. **Use exponential backoff** - Give services time to recover
3. **Add jitter** - Prevent thundering herd from synchronized retries
4. **Cap total duration** - `stop_after_attempt(5) | stop_after_delay(60)`
5. **Log every retry** - Silent retries hide systemic problems
6. **Use decorators** - Keep retry logic separate from business logic
7. **Inject dependencies** - Make infrastructure testable
8. **Set timeouts everywhere** - Every network call needs a timeout
9. **Fail gracefully** - Return cached/default values for non-critical paths
10. **Monitor retry rates** - High retry rates indicate underlying issues

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
