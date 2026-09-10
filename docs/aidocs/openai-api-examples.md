# OpenAI Python 库 API 调用示例

!!! abstract "概述"
    本文档展示如何使用 OpenAI Python 库调用不同 AI 模型的 API，包括 Anthropic Claude、OpenAI Codex 和 xAI Grok。通过统一的接口，您可以轻松切换不同的 AI 服务提供商。

---

## 引言

OpenAI Python 库提供了一个标准化的接口来调用各种 AI 模型，主人。许多 AI 服务提供商都采用了 OpenAI 兼容的 API 格式，这使得我们可以使用相同的代码结构来调用不同的模型，主人。

### 为什么使用 OpenAI Python 库？

> "统一的 API 接口让 AI 集成变得简单高效。"

**核心优势：**

- :material-api: **统一接口**：一套代码适配多个 AI 提供商
- :material-swap-horizontal: **易于切换**：快速在不同模型之间切换
- :material-code-braces: **类型提示**：完整的类型注解支持
- :material-shield-check: **错误处理**：完善的异常处理机制
- :material-lightning-bolt: **流式响应**：支持实时流式输出
- :material-sync: **异步支持**：支持异步编程模式

---

## 环境准备

### 安装依赖

首先需要安装 OpenAI Python 库，主人：

```bash title="安装命令"
# 安装最新版本
pip install openai

# 或指定版本
pip install openai>=1.0.0
```

### 配置 API 密钥

=== "环境变量方式（推荐）"
    **Linux / macOS / WSL：**
    ```bash
    # 临时设置
    export ANTHROPIC_API_KEY="your-anthropic-key"
    export OPENAI_API_KEY="your-openai-key"
    export XAI_API_KEY="your-xai-key"
    
    # 永久设置（添加到 ~/.bashrc）
    echo 'export ANTHROPIC_API_KEY="your-anthropic-key"' >> ~/.bashrc
    echo 'export OPENAI_API_KEY="your-openai-key"' >> ~/.bashrc
    echo 'export XAI_API_KEY="your-xai-key"' >> ~/.bashrc
    source ~/.bashrc
    ```
    
    **Windows PowerShell：**
    ```powershell
    # 临时设置
    $env:ANTHROPIC_API_KEY = "your-anthropic-key"
    $env:OPENAI_API_KEY = "your-openai-key"
    $env:XAI_API_KEY = "your-xai-key"
    
    # 永久设置
    [System.Environment]::SetEnvironmentVariable('ANTHROPIC_API_KEY', 'your-anthropic-key', 'User')
    [System.Environment]::SetEnvironmentVariable('OPENAI_API_KEY', 'your-openai-key', 'User')
    [System.Environment]::SetEnvironmentVariable('XAI_API_KEY', 'your-xai-key', 'User')
    ```

=== "代码中直接配置"
    ```python
    import os
    
    # 在代码中设置（不推荐用于生产环境）
    os.environ['ANTHROPIC_API_KEY'] = 'your-anthropic-key'
    os.environ['OPENAI_API_KEY'] = 'your-openai-key'
    os.environ['XAI_API_KEY'] = 'your-xai-key'
    ```

=== ".env 文件方式"
    创建 `.env` 文件：
    ```ini title=".env"
    ANTHROPIC_API_KEY=your-anthropic-key
    OPENAI_API_KEY=your-openai-key
    XAI_API_KEY=your-xai-key
    ```
    
    使用 python-dotenv 加载：
    ```python
    from dotenv import load_dotenv
    import os
    
    # 加载 .env 文件
    load_dotenv()
    
    # 访问环境变量
    anthropic_key = os.getenv('ANTHROPIC_API_KEY')
    ```

---

## Claude API 示例

### 基础调用

Anthropic Claude 是一个强大的 AI 助手，支持长上下文和多轮对话，主人。

```python title="claude_basic.py" linenums="1"
#!/usr/bin/env python3
"""
Claude API 基础示例
使用 OpenAI 兼容的接口调用 Anthropic Claude
"""

from openai import OpenAI
import os

def test_claude_basic():
    """Claude 基础对话测试"""
    
    # 初始化客户端
    client = OpenAI(
        api_key=os.environ.get("ANTHROPIC_API_KEY"),
        base_url="https://api.anthropic.com/v1"
    )
    
    # 发送请求
    response = client.chat.completions.create(
        model="claude-3-5-sonnet-20241022",  # 或 claude-3-opus-20240229
        messages=[
            {
                "role": "user",
                "content": "用中文解释什么是机器学习，不超过100字。"
            }
        ],
        max_tokens=1024,
        temperature=0.7
    )
    
    # 输出结果
    print("Claude 回复：")
    print(response.choices[0].message.content)
    print(f"\n使用的 tokens: {response.usage.total_tokens}")

if __name__ == "__main__":
    test_claude_basic()
```

### 多轮对话

```python title="claude_conversation.py" linenums="1"
#!/usr/bin/env python3
"""
Claude 多轮对话示例
展示如何维护对话上下文
"""

from openai import OpenAI
import os

def test_claude_conversation():
    """Claude 多轮对话测试"""
    
    client = OpenAI(
        api_key=os.environ.get("ANTHROPIC_API_KEY"),
        base_url="https://api.anthropic.com/v1"
    )
    
    # 对话历史
    conversation = [
        {"role": "user", "content": "我想学习 Python，从哪里开始？"},
    ]
    
    # 第一轮对话
    response = client.chat.completions.create(
        model="claude-3-5-sonnet-20241022",
        messages=conversation,
        max_tokens=1024
    )
    
    assistant_reply = response.choices[0].message.content
    print("用户：我想学习 Python，从哪里开始？")
    print(f"Claude：{assistant_reply}\n")
    
    # 添加助手回复到历史
    conversation.append({"role": "assistant", "content": assistant_reply})
    
    # 第二轮对话
    conversation.append({"role": "user", "content": "推荐几本适合初学者的书籍。"})
    
    response = client.chat.completions.create(
        model="claude-3-5-sonnet-20241022",
        messages=conversation,
        max_tokens=1024
    )
    
    print("用户：推荐几本适合初学者的书籍。")
    print(f"Claude：{response.choices[0].message.content}")

if __name__ == "__main__":
    test_claude_conversation()
```

### 流式输出

```python title="claude_streaming.py" linenums="1"
#!/usr/bin/env python3
"""
Claude 流式输出示例
实时接收 AI 生成的内容
"""

from openai import OpenAI
import os
import sys

def test_claude_streaming():
    """Claude 流式输出测试"""
    
    client = OpenAI(
        api_key=os.environ.get("ANTHROPIC_API_KEY"),
        base_url="https://api.anthropic.com/v1"
    )
    
    print("Claude 正在生成回复...\n")
    
    # 启用流式输出
    stream = client.chat.completions.create(
        model="claude-3-5-sonnet-20241022",
        messages=[
            {
                "role": "user",
                "content": "写一首关于春天的中文短诗。"
            }
        ],
        max_tokens=512,
        stream=True  # 启用流式输出
    )
    
    # 逐块接收并输出
    for chunk in stream:
        if chunk.choices[0].delta.content is not None:
            content = chunk.choices[0].delta.content
            print(content, end='', flush=True)
            sys.stdout.flush()
    
    print("\n\n流式输出完成！")

if __name__ == "__main__":
    test_claude_streaming()
```

---

## OpenAI Codex 示例

### 代码生成

OpenAI Codex 专注于代码生成和理解，主人。

```python title="codex_basic.py" linenums="1"
#!/usr/bin/env python3
"""
OpenAI Codex 代码生成示例
使用 GPT-4 或 GPT-3.5-turbo 进行代码生成
"""

from openai import OpenAI
import os

def test_codex_code_generation():
    """Codex 代码生成测试"""
    
    client = OpenAI(
        api_key=os.environ.get("OPENAI_API_KEY")
    )
    
    # 代码生成请求
    response = client.chat.completions.create(
        model="gpt-4",  # 或 "gpt-3.5-turbo"
        messages=[
            {
                "role": "system",
                "content": "你是一个专业的 Python 程序员，擅长编写清晰、高效的代码。"
            },
            {
                "role": "user",
                "content": """
写一个 Python 函数，实现二分查找算法。
要求：
1. 包含详细的文档字符串
2. 添加类型注解
3. 包含边界条件处理
                """
            }
        ],
        temperature=0.2,  # 较低的温度以获得更确定的代码
        max_tokens=1024
    )
    
    print("生成的代码：\n")
    print(response.choices[0].message.content)

if __name__ == "__main__":
    test_codex_code_generation()
```

### 代码解释

```python title="codex_explain.py" linenums="1"
#!/usr/bin/env python3
"""
OpenAI Codex 代码解释示例
让 AI 解释代码的功能
"""

from openai import OpenAI
import os

def test_codex_code_explanation():
    """Codex 代码解释测试"""
    
    client = OpenAI(
        api_key=os.environ.get("OPENAI_API_KEY")
    )
    
    code_to_explain = """
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)
    """
    
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[
            {
                "role": "system",
                "content": "你是一个代码导师，擅长用通俗易懂的语言解释代码。"
            },
            {
                "role": "user",
                "content": f"请用中文详细解释这段代码的工作原理：\n\n```python\n{code_to_explain}\n```"
            }
        ],
        temperature=0.3,
        max_tokens=1024
    )
    
    print("代码解释：\n")
    print(response.choices[0].message.content)

if __name__ == "__main__":
    test_codex_code_explanation()
```

### 代码调试

```python title="codex_debug.py" linenums="1"
#!/usr/bin/env python3
"""
OpenAI Codex 代码调试示例
让 AI 帮助找出并修复代码中的错误
"""

from openai import OpenAI
import os

def test_codex_debugging():
    """Codex 代码调试测试"""
    
    client = OpenAI(
        api_key=os.environ.get("OPENAI_API_KEY")
    )
    
    buggy_code = """
def calculate_average(numbers):
    total = 0
    for num in numbers:
        total += num
    return total / len(numbers)

# 测试
result = calculate_average([])
print(f"平均值: {result}")
    """
    
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[
            {
                "role": "system",
                "content": "你是一个代码调试专家，擅长发现并修复代码中的 bug。"
            },
            {
                "role": "user",
                "content": f"""
这段代码有问题，请：
1. 指出问题所在
2. 解释为什么会出错
3. 提供修复后的代码

代码：
```python
{buggy_code}
```
                """
            }
        ],
        temperature=0.2,
        max_tokens=1024
    )
    
    print("调试分析：\n")
    print(response.choices[0].message.content)

if __name__ == "__main__":
    test_codex_debugging()
```

---

## Grok (xAI) 示例

### 基础调用

Grok 是 xAI 开发的 AI 模型，以其实时信息和幽默风格著称，主人。

```python title="grok_basic.py" linenums="1"
#!/usr/bin/env python3
"""
Grok API 基础示例
使用 OpenAI 兼容的接口调用 xAI Grok
"""

from openai import OpenAI
import os

def test_grok_basic():
    """Grok 基础对话测试"""
    
    client = OpenAI(
        api_key=os.environ.get("XAI_API_KEY"),
        base_url="https://api.x.ai/v1"
    )
    
    response = client.chat.completions.create(
        model="grok-beta",
        messages=[
            {
                "role": "user",
                "content": "用中文解释什么是大语言模型，要有趣一点。"
            }
        ],
        temperature=0.8,  # Grok 适合稍高的温度以展现个性
        max_tokens=1024
    )
    
    print("Grok 回复：")
    print(response.choices[0].message.content)
    print(f"\n使用的 tokens: {response.usage.total_tokens}")

if __name__ == "__main__":
    test_grok_basic()
```

### 实时信息查询

```python title="grok_realtime.py" linenums="1"
#!/usr/bin/env python3
"""
Grok 实时信息查询示例
Grok 能够访问实时数据
"""

from openai import OpenAI
import os

def test_grok_realtime():
    """Grok 实时信息查询测试"""
    
    client = OpenAI(
        api_key=os.environ.get("XAI_API_KEY"),
        base_url="https://api.x.ai/v1"
    )
    
    response = client.chat.completions.create(
        model="grok-beta",
        messages=[
            {
                "role": "system",
                "content": "你可以访问实时信息，请用中文回答问题。"
            },
            {
                "role": "user",
                "content": "当前科技领域有什么热门话题？列举3个并简要说明。"
            }
        ],
        temperature=0.7,
        max_tokens=1024
    )
    
    print("Grok 实时信息：\n")
    print(response.choices[0].message.content)

if __name__ == "__main__":
    test_grok_realtime()
```

### 图像理解（Grok Vision）

```python title="grok_vision.py" linenums="1"
#!/usr/bin/env python3
"""
Grok Vision 图像理解示例
使用 Grok 的视觉能力分析图像
"""

from openai import OpenAI
import os
import base64

def encode_image(image_path):
    """将图像编码为 base64"""
    with open(image_path, "rb") as image_file:
        return base64.b64encode(image_file.read()).decode('utf-8')

def test_grok_vision():
    """Grok 图像理解测试"""
    
    client = OpenAI(
        api_key=os.environ.get("XAI_API_KEY"),
        base_url="https://api.x.ai/v1"
    )
    
    # 方式1：使用图像 URL
    response = client.chat.completions.create(
        model="grok-vision-beta",
        messages=[
            {
                "role": "user",
                "content": [
                    {
                        "type": "text",
                        "text": "请用中文描述这张图片的内容。"
                    },
                    {
                        "type": "image_url",
                        "image_url": {
                            "url": "https://example.com/image.jpg"
                        }
                    }
                ]
            }
        ],
        max_tokens=1024
    )
    
    print("Grok Vision 分析：\n")
    print(response.choices[0].message.content)
    
    # 方式2：使用本地图像（base64 编码）
    # base64_image = encode_image("path/to/local/image.jpg")
    # image_url = f"data:image/jpeg;base64,{base64_image}"
    # 然后在上面的代码中使用这个 image_url

if __name__ == "__main__":
    test_grok_vision()
```

---

## 完整示例：模型对比

### 统一接口对比测试

```python title="model_comparison.py" linenums="1"
#!/usr/bin/env python3
"""
多模型对比示例
使用相同的问题测试不同的 AI 模型
"""

from openai import OpenAI
import os
from typing import Dict, List
import time

class AIModelTester:
    """AI 模型测试器"""
    
    def __init__(self):
        """初始化所有模型客户端"""
        self.models = {
            "Claude": {
                "client": OpenAI(
                    api_key=os.environ.get("ANTHROPIC_API_KEY"),
                    base_url="https://api.anthropic.com/v1"
                ),
                "model": "claude-3-5-sonnet-20241022"
            },
            "GPT-4": {
                "client": OpenAI(
                    api_key=os.environ.get("OPENAI_API_KEY")
                ),
                "model": "gpt-4"
            },
            "Grok": {
                "client": OpenAI(
                    api_key=os.environ.get("XAI_API_KEY"),
                    base_url="https://api.x.ai/v1"
                ),
                "model": "grok-beta"
            }
        }
    
    def test_model(self, model_name: str, prompt: str) -> Dict:
        """测试单个模型"""
        print(f"\n{'='*60}")
        print(f"测试模型: {model_name}")
        print(f"{'='*60}")
        
        config = self.models[model_name]
        start_time = time.time()
        
        try:
            response = config["client"].chat.completions.create(
                model=config["model"],
                messages=[
                    {
                        "role": "user",
                        "content": prompt
                    }
                ],
                temperature=0.7,
                max_tokens=512
            )
            
            elapsed_time = time.time() - start_time
            
            result = {
                "model": model_name,
                "content": response.choices[0].message.content,
                "tokens": response.usage.total_tokens,
                "time": elapsed_time,
                "success": True
            }
            
            print(f"回复内容:\n{result['content']}")
            print(f"\n统计信息:")
            print(f"  - 使用 tokens: {result['tokens']}")
            print(f"  - 响应时间: {result['time']:.2f} 秒")
            
            return result
            
        except Exception as e:
            print(f"错误: {str(e)}")
            return {
                "model": model_name,
                "success": False,
                "error": str(e)
            }
    
    def compare_all(self, prompt: str):
        """对比所有模型"""
        print("\n" + "="*60)
        print("开始多模型对比测试")
        print("="*60)
        print(f"测试问题: {prompt}\n")
        
        results = []
        for model_name in self.models.keys():
            result = self.test_model(model_name, prompt)
            results.append(result)
            time.sleep(1)  # 避免请求过快
        
        # 输出对比总结
        print("\n" + "="*60)
        print("对比总结")
        print("="*60)
        
        for result in results:
            if result["success"]:
                print(f"\n{result['model']}:")
                print(f"  - Tokens: {result['tokens']}")
                print(f"  - 时间: {result['time']:.2f}s")
                print(f"  - 响应长度: {len(result['content'])} 字符")

def main():
    """主函数"""
    tester = AIModelTester()
    
    # 测试问题
    test_prompts = [
        "用一句话解释什么是量子计算。",
        "写一个 Python 函数来计算斐波那契数列。",
        "给我3个提高编程效率的建议。"
    ]
    
    # 选择一个问题进行测试
    prompt = test_prompts[0]
    tester.compare_all(prompt)

if __name__ == "__main__":
    main()
```

---

## 高级技巧

### 错误处理

```python title="error_handling.py" linenums="1"
#!/usr/bin/env python3
"""
错误处理示例
展示如何优雅地处理 API 调用中的错误
"""

from openai import OpenAI, APIError, APIConnectionError, RateLimitError
import os
import time

def robust_api_call(client, model, messages, max_retries=3):
    """带重试机制的 API 调用"""
    
    for attempt in range(max_retries):
        try:
            response = client.chat.completions.create(
                model=model,
                messages=messages,
                timeout=30.0  # 设置超时
            )
            return response
            
        except RateLimitError as e:
            print(f"速率限制错误，等待后重试... (尝试 {attempt + 1}/{max_retries})")
            time.sleep(2 ** attempt)  # 指数退避
            
        except APIConnectionError as e:
            print(f"连接错误: {e}")
            if attempt < max_retries - 1:
                time.sleep(1)
                
        except APIError as e:
            print(f"API 错误: {e}")
            break
            
        except Exception as e:
            print(f"未知错误: {e}")
            break
    
    return None

def main():
    """主函数"""
    client = OpenAI(
        api_key=os.environ.get("OPENAI_API_KEY")
    )
    
    messages = [
        {"role": "user", "content": "Hello!"}
    ]
    
    response = robust_api_call(client, "gpt-4", messages)
    
    if response:
        print("成功获取响应:")
        print(response.choices[0].message.content)
    else:
        print("所有重试均失败")

if __name__ == "__main__":
    main()
```

### 异步调用

```python title="async_example.py" linenums="1"
#!/usr/bin/env python3
"""
异步调用示例
使用异步方式同时调用多个模型
"""

import asyncio
from openai import AsyncOpenAI
import os

async def call_claude(prompt: str):
    """异步调用 Claude"""
    client = AsyncOpenAI(
        api_key=os.environ.get("ANTHROPIC_API_KEY"),
        base_url="https://api.anthropic.com/v1"
    )
    
    response = await client.chat.completions.create(
        model="claude-3-5-sonnet-20241022",
        messages=[{"role": "user", "content": prompt}]
    )
    
    return {
        "model": "Claude",
        "response": response.choices[0].message.content
    }

async def call_gpt4(prompt: str):
    """异步调用 GPT-4"""
    client = AsyncOpenAI(
        api_key=os.environ.get("OPENAI_API_KEY")
    )
    
    response = await client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    
    return {
        "model": "GPT-4",
        "response": response.choices[0].message.content
    }

async def call_grok(prompt: str):
    """异步调用 Grok"""
    client = AsyncOpenAI(
        api_key=os.environ.get("XAI_API_KEY"),
        base_url="https://api.x.ai/v1"
    )
    
    response = await client.chat.completions.create(
        model="grok-beta",
        messages=[{"role": "user", "content": prompt}]
    )
    
    return {
        "model": "Grok",
        "response": response.choices[0].message.content
    }

async def main():
    """主函数 - 并发调用所有模型"""
    prompt = "用一句话解释什么是深度学习。"
    
    print(f"问题: {prompt}\n")
    print("正在并发调用所有模型...\n")
    
    # 并发执行所有调用
    results = await asyncio.gather(
        call_claude(prompt),
        call_gpt4(prompt),
        call_grok(prompt),
        return_exceptions=True
    )
    
    # 输出结果
    for result in results:
        if isinstance(result, dict):
            print(f"{result['model']} 的回复:")
            print(result['response'])
            print("\n" + "-"*60 + "\n")
        else:
            print(f"错误: {result}")

if __name__ == "__main__":
    asyncio.run(main())
```

---

## 最佳实践

### 参数调优指南

不同的任务需要不同的参数设置，主人：

| 参数 | 创意写作 | 代码生成 | 数据分析 | 翻译任务 |
|------|---------|---------|---------|---------|
| **temperature** | 0.8-1.0 | 0.2-0.3 | 0.3-0.5 | 0.3 |
| **max_tokens** | 1024-2048 | 512-1024 | 512-1024 | 512-1024 |
| **top_p** | 0.9-1.0 | 0.9 | 0.9 | 0.9 |

### 提示词优化技巧

!!! tip "提示词最佳实践"
    1. **明确角色**：在 system 消息中定义 AI 的角色
    2. **具体指令**：给出清晰、具体的任务描述
    3. **提供示例**：使用 few-shot learning 提供示例
    4. **结构化输出**：指定期望的输出格式
    5. **设置约束**：明确字数、风格等限制

### 成本优化建议

```python title="cost_optimization.py" linenums="1"
#!/usr/bin/env python3
"""
成本优化示例
展示如何在保证质量的前提下降低成本
"""

from openai import OpenAI
import os

def cost_effective_api_call():
    """成本优化的 API 调用"""
    client = OpenAI(
        api_key=os.environ.get("OPENAI_API_KEY")
    )
    
    # 策略1: 使用更经济的模型
    # GPT-3.5-turbo 比 GPT-4 便宜很多，适合简单任务
    response = client.chat.completions.create(
        model="gpt-3.5-turbo",  # 而不是 "gpt-4"
        messages=[
            {"role": "user", "content": "总结这段文本..."}
        ],
        max_tokens=256,  # 策略2: 限制输出长度
        temperature=0.3   # 策略3: 降低温度减少随机性
    )
    
    return response

# 策略4: 缓存常见查询
cache = {}

def cached_api_call(prompt):
    """带缓存的 API 调用"""
    if prompt in cache:
        print("从缓存返回结果")
        return cache[prompt]
    
    # 实际调用 API
    # response = ...
    # cache[prompt] = response
    # return response
    pass

if __name__ == "__main__":
    cost_effective_api_call()
```

---

## 常见问题

### Q1: 如何选择合适的模型？

??? question "模型选择指南"
    **Claude**：
    - ✅ 长文本处理（支持 200K tokens）
    - ✅ 复杂推理任务
    - ✅ 代码分析和生成
    - ✅ 安全性要求高的场景
    
    **GPT-4**：
    - ✅ 通用任务
    - ✅ 多语言支持
    - ✅ 创意写作
    - ✅ 复杂问题解决
    
    **Grok**：
    - ✅ 需要实时信息
    - ✅ 轻松幽默的回复
    - ✅ 图像理解（vision 版本）

### Q2: API 调用失败怎么办？

??? question "故障排查步骤"
    1. **检查 API 密钥**：确保环境变量正确设置
    2. **验证网络连接**：测试能否访问 API 端点
    3. **查看错误信息**：根据错误类型采取相应措施
    4. **实现重试机制**：使用指数退避策略
    5. **监控配额**：检查是否超过速率限制

### Q3: 如何处理超长文本？

??? question "长文本处理方案"
    ```python
    def process_long_text(text, max_chunk_size=4000):
        """将长文本分块处理"""
        chunks = [text[i:i+max_chunk_size] 
                  for i in range(0, len(text), max_chunk_size)]
        
        results = []
        for chunk in chunks:
            # 处理每个分块
            response = client.chat.completions.create(
                model="gpt-4",
                messages=[
                    {"role": "user", "content": f"总结：{chunk}"}
                ]
            )
            results.append(response.choices[0].message.content)
        
        # 合并结果
        return "\n\n".join(results)
    ```

---

## 总结

本文档展示了如何使用 OpenAI Python 库调用 Claude、GPT-4 和 Grok 三种主流 AI 模型，主人。

### 关键要点

:material-check-circle: **统一接口**：所有模型使用相同的代码结构，主人

:material-check-circle: **灵活切换**：轻松在不同模型之间切换，主人

:material-check-circle: **完整示例**：涵盖基础、进阶和实战场景，主人

:material-check-circle: **最佳实践**：包含错误处理、异步调用等高级技巧，主人

### 推荐学习路径

1. **基础入门**：从单个模型的基础调用开始，主人
2. **功能探索**：尝试流式输出、多轮对话等功能，主人
3. **进阶应用**：学习异步调用、错误处理等高级技巧，主人
4. **实战项目**：将 API 集成到实际项目中，主人

---

## 参考资源

!!! info "官方文档"
    - 📘 [OpenAI API Documentation](https://platform.openai.com/docs/api-reference)
    - 📘 [Anthropic Claude API](https://docs.anthropic.com/claude/reference/getting-started-with-the-api)
    - 📘 [xAI Grok API](https://docs.x.ai/api)
    - 📘 [OpenAI Python Library](https://github.com/openai/openai-python)

---

<div style="text-align: center; margin-top: 50px; padding: 20px; background-color: #f5f5f5; border-radius: 8px;">
    <p style="font-size: 14px; color: #666;">
        📝 本文档最后更新于 2026年8月31日<br>
        ✍️ 整理：RexCore AI文档小组<br>
        🔗 OpenAI Python 库版本：1.0+
    </p>
</div>
