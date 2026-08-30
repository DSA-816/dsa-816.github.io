# 链接与引用展示方法

本页面展示了 Zensical 文档系统中各种创建和美化外链的方法。

---

## 基本链接语法

### 行内链接

最基本的 Markdown 链接语法：

```markdown
[Zensical 官方文档](https://zensical.org)
```

效果：[Zensical 官方文档](https://zensical.org)

### 带标题的链接

鼠标悬停时显示提示文字：

```markdown
[GitHub](https://github.com "全球最大的代码托管平台")
```

效果：[GitHub](https://github.com "全球最大的代码托管平台")

### 自动链接

直接显示 URL：

```markdown
<https://www.google.com>
```

效果：<https://www.google.com>

---

## 参考式链接

将链接定义与使用分离，便于管理：

```markdown
这是一个 [参考式链接][ref1]，还有 [另一个][ref2]。

[ref1]: https://zensical.org
[ref2]: https://github.com
```

效果：

这是一个 [参考式链接][ref1]，还有 [另一个][ref2]。

[ref1]: https://zensical.org
[ref2]: https://github.com

---

## 在新标签页打开

使用 HTML 属性控制链接行为：

```markdown
[在新标签页打开 Google](https://www.google.com){target="_blank"}
```

效果：[在新标签页打开 Google](https://www.google.com){target="_blank"}

---

## 按钮样式链接

### 简洁按钮

```html
<a href="https://zensical.org" style="display: inline-block; padding: 10px 20px; background-color: #4051B5; color: white; text-decoration: none; border-radius: 5px; font-weight: 500;">
  访问 Zensical
</a>
```

效果：

<a href="https://zensical.org" style="display: inline-block; padding: 10px 20px; background-color: #4051B5; color: white; text-decoration: none; border-radius: 5px; font-weight: 500;">
  访问 Zensical
</a>

### 多种按钮样式

```html
<div style="display: flex; gap: 10px; flex-wrap: wrap; margin: 15px 0;">
  <a href="https://github.com" style="display: inline-block; padding: 8px 16px; background-color: #24292e; color: white; text-decoration: none; border-radius: 6px; font-size: 14px;">
    🐙 GitHub
  </a>
  <a href="https://www.python.org" style="display: inline-block; padding: 8px 16px; background-color: #3776ab; color: white; text-decoration: none; border-radius: 6px; font-size: 14px;">
    🐍 Python
  </a>
  <a href="https://www.google.com" style="display: inline-block; padding: 8px 16px; background-color: #4285f4; color: white; text-decoration: none; border-radius: 6px; font-size: 14px;">
    🔍 Google
  </a>
</div>
```

效果：

<div style="display: flex; gap: 10px; flex-wrap: wrap; margin: 15px 0;">
  <a href="https://github.com" style="display: inline-block; padding: 8px 16px; background-color: #24292e; color: white; text-decoration: none; border-radius: 6px; font-size: 14px;">
    🐙 GitHub
  </a>
  <a href="https://www.python.org" style="display: inline-block; padding: 8px 16px; background-color: #3776ab; color: white; text-decoration: none; border-radius: 6px; font-size: 14px;">
    🐍 Python
  </a>
  <a href="https://www.google.com" style="display: inline-block; padding: 8px 16px; background-color: #4285f4; color: white; text-decoration: none; border-radius: 6px; font-size: 14px;">
    🔍 Google
  </a>
</div>

### 轮廓按钮

```html
<a href="https://zensical.org" style="display: inline-block; padding: 10px 20px; border: 2px solid #4051B5; color: #4051B5; text-decoration: none; border-radius: 5px; font-weight: 500; transition: all 0.3s;">
  了解更多
</a>
```

效果：

<a href="https://zensical.org" style="display: inline-block; padding: 10px 20px; border: 2px solid #4051B5; color: #4051B5; text-decoration: none; border-radius: 5px; font-weight: 500;">
  了解更多
</a>

---

## 卡片式链接

### 基础卡片

```html
<a href="https://zensical.org" style="display: block; padding: 20px; border: 1px solid #e0e0e0; border-radius: 8px; text-decoration: none; color: inherit; transition: box-shadow 0.3s;" onmouseover="this.style.boxShadow='0 4px 12px rgba(0,0,0,0.15)'" onmouseout="this.style.boxShadow='none'">
  <h3 style="margin: 0 0 10px 0; color: #4051B5;">📚 Zensical 文档</h3>
  <p style="margin: 0; color: #666; font-size: 14px;">强大的技术文档生成工具，基于 Material for MkDocs。</p>
</a>
```

效果：

<a href="https://zensical.org" style="display: block; padding: 20px; border: 1px solid #e0e0e0; border-radius: 8px; text-decoration: none; color: inherit; transition: box-shadow 0.3s; margin: 15px 0;" onmouseover="this.style.boxShadow='0 4px 12px rgba(0,0,0,0.15)'" onmouseout="this.style.boxShadow='none'">
  <h3 style="margin: 0 0 10px 0; color: #4051B5;">📚 Zensical 文档</h3>
  <p style="margin: 0; color: #666; font-size: 14px;">强大的技术文档生成工具，基于 Material for MkDocs。</p>
</a>

### 卡片网格

```html
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 15px; margin: 20px 0;">
  <a href="https://github.com" style="display: block; padding: 20px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 10px; text-decoration: none; color: white;">
    <div style="font-size: 32px; margin-bottom: 10px;">🐙</div>
    <h4 style="margin: 0 0 8px 0;">GitHub</h4>
    <p style="margin: 0; font-size: 13px; opacity: 0.9;">代码托管平台</p>
  </a>
  
  <a href="https://stackoverflow.com" style="display: block; padding: 20px; background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); border-radius: 10px; text-decoration: none; color: white;">
    <div style="font-size: 32px; margin-bottom: 10px;">💬</div>
    <h4 style="margin: 0 0 8px 0;">Stack Overflow</h4>
    <p style="margin: 0; font-size: 13px; opacity: 0.9;">程序员问答社区</p>
  </a>
  
  <a href="https://www.python.org" style="display: block; padding: 20px; background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); border-radius: 10px; text-decoration: none; color: white;">
    <div style="font-size: 32px; margin-bottom: 10px;">🐍</div>
    <h4 style="margin: 0 0 8px 0;">Python</h4>
    <p style="margin: 0; font-size: 13px; opacity: 0.9;">官方网站</p>
  </a>
</div>
```

效果：

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 15px; margin: 20px 0;">
  <a href="https://github.com" style="display: block; padding: 20px; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); border-radius: 10px; text-decoration: none; color: white;">
    <div style="font-size: 32px; margin-bottom: 10px;">🐙</div>
    <h4 style="margin: 0 0 8px 0;">GitHub</h4>
    <p style="margin: 0; font-size: 13px; opacity: 0.9;">代码托管平台</p>
  </a>
  
  <a href="https://stackoverflow.com" style="display: block; padding: 20px; background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); border-radius: 10px; text-decoration: none; color: white;">
    <div style="font-size: 32px; margin-bottom: 10px;">💬</div>
    <h4 style="margin: 0 0 8px 0;">Stack Overflow</h4>
    <p style="margin: 0; font-size: 13px; opacity: 0.9;">程序员问答社区</p>
  </a>
  
  <a href="https://www.python.org" style="display: block; padding: 20px; background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); border-radius: 10px; text-decoration: none; color: white;">
    <div style="font-size: 32px; margin-bottom: 10px;">🐍</div>
    <h4 style="margin: 0 0 8px 0;">Python</h4>
    <p style="margin: 0; font-size: 13px; opacity: 0.9;">官方网站</p>
  </a>
</div>

---

## 图标链接

### 简洁图标链接

```markdown
:material-github: [GitHub](https://github.com)  
:material-twitter: [Twitter](https://twitter.com)  
:material-linkedin: [LinkedIn](https://linkedin.com)
```

效果：

:material-github: [GitHub](https://github.com)  
:material-twitter: [Twitter](https://twitter.com)  
:material-linkedin: [LinkedIn](https://linkedin.com)

### 社交媒体链接栏

```html
<div style="display: flex; gap: 15px; margin: 20px 0;">
  <a href="https://github.com" style="display: flex; align-items: center; justify-content: center; width: 40px; height: 40px; background-color: #24292e; color: white; text-decoration: none; border-radius: 50%; font-size: 20px;">
    <span>🐙</span>
  </a>
  <a href="https://twitter.com" style="display: flex; align-items: center; justify-content: center; width: 40px; height: 40px; background-color: #1DA1F2; color: white; text-decoration: none; border-radius: 50%; font-size: 20px;">
    <span>🐦</span>
  </a>
  <a href="https://linkedin.com" style="display: flex; align-items: center; justify-content: center; width: 40px; height: 40px; background-color: #0077B5; color: white; text-decoration: none; border-radius: 50%; font-size: 20px;">
    <span>💼</span>
  </a>
  <a href="https://youtube.com" style="display: flex; align-items: center; justify-content: center; width: 40px; height: 40px; background-color: #FF0000; color: white; text-decoration: none; border-radius: 50%; font-size: 20px;">
    <span>📺</span>
  </a>
</div>
```

效果：

<div style="display: flex; gap: 15px; margin: 20px 0;">
  <a href="https://github.com" style="display: flex; align-items: center; justify-content: center; width: 40px; height: 40px; background-color: #24292e; color: white; text-decoration: none; border-radius: 50%; font-size: 20px;">
    <span>🐙</span>
  </a>
  <a href="https://twitter.com" style="display: flex; align-items: center; justify-content: center; width: 40px; height: 40px; background-color: #1DA1F2; color: white; text-decoration: none; border-radius: 50%; font-size: 20px;">
    <span>🐦</span>
  </a>
  <a href="https://linkedin.com" style="display: flex; align-items: center; justify-content: center; width: 40px; height: 40px; background-color: #0077B5; color: white; text-decoration: none; border-radius: 50%; font-size: 20px;">
    <span>💼</span>
  </a>
  <a href="https://youtube.com" style="display: flex; align-items: center; justify-content: center; width: 40px; height: 40px; background-color: #FF0000; color: white; text-decoration: none; border-radius: 50%; font-size: 20px;">
    <span>📺</span>
  </a>
</div>

---

## 使用 Admonition 展示链接

### 提示框链接

!!! tip "推荐资源"
    - [Zensical 官方文档](https://zensical.org) - 完整的使用指南
    - [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) - 底层框架文档

!!! info "相关链接"
    访问 [GitHub 仓库](https://github.com) 查看源代码  
    查看 [在线演示](https://example.com) 了解更多

!!! example "实用工具"
    :material-web: [Google](https://www.google.com) - 搜索引擎  
    :material-translate: [DeepL](https://www.deepl.com) - 翻译工具  
    :material-palette: [Coolors](https://coolors.co) - 配色方案

---

## 使用 Tabs 分类链接

=== "开发工具"
    - [Visual Studio Code](https://code.visualstudio.com) - 代码编辑器
    - [Git](https://git-scm.com) - 版本控制
    - [Docker](https://www.docker.com) - 容器化平台
    - [Postman](https://www.postman.com) - API 测试工具

=== "学习资源"
    - [MDN Web Docs](https://developer.mozilla.org) - Web 开发文档
    - [W3Schools](https://www.w3schools.com) - 在线教程
    - [freeCodeCamp](https://www.freecodecamp.org) - 免费编程课程
    - [Coursera](https://www.coursera.org) - 在线课程平台

=== "社区论坛"
    - [Stack Overflow](https://stackoverflow.com) - 技术问答
    - [Reddit Programming](https://www.reddit.com/r/programming/) - 编程社区
    - [DEV Community](https://dev.to) - 开发者社区
    - [Hacker News](https://news.ycombinator.com) - 科技新闻

=== "设计资源"
    - [Dribbble](https://dribbble.com) - 设计作品展示
    - [Behance](https://www.behance.net) - 创意作品平台
    - [Figma](https://www.figma.com) - 协作设计工具
    - [Unsplash](https://unsplash.com) - 免费图片库

---

## 链接列表样式

### 简洁列表

```html
<div style="border-left: 4px solid #4051B5; padding-left: 20px; margin: 20px 0;">
  <p style="margin: 8px 0;"><a href="https://github.com" style="color: #4051B5; text-decoration: none;">→ GitHub</a></p>
  <p style="margin: 8px 0;"><a href="https://stackoverflow.com" style="color: #4051B5; text-decoration: none;">→ Stack Overflow</a></p>
  <p style="margin: 8px 0;"><a href="https://developer.mozilla.org" style="color: #4051B5; text-decoration: none;">→ MDN Web Docs</a></p>
</div>
```

效果：

<div style="border-left: 4px solid #4051B5; padding-left: 20px; margin: 20px 0;">
  <p style="margin: 8px 0;"><a href="https://github.com" style="color: #4051B5; text-decoration: none;">→ GitHub</a></p>
  <p style="margin: 8px 0;"><a href="https://stackoverflow.com" style="color: #4051B5; text-decoration: none;">→ Stack Overflow</a></p>
  <p style="margin: 8px 0;"><a href="https://developer.mozilla.org" style="color: #4051B5; text-decoration: none;">→ MDN Web Docs</a></p>
</div>

### 带描述的列表

```html
<div style="margin: 20px 0;">
  <div style="padding: 15px; border: 1px solid #e0e0e0; border-radius: 8px; margin-bottom: 10px;">
    <a href="https://zensical.org" style="font-weight: 600; color: #4051B5; text-decoration: none; font-size: 16px;">Zensical</a>
    <p style="margin: 5px 0 0 0; color: #666; font-size: 14px;">技术文档生成工具，简单高效</p>
  </div>
  
  <div style="padding: 15px; border: 1px solid #e0e0e0; border-radius: 8px; margin-bottom: 10px;">
    <a href="https://www.python.org" style="font-weight: 600; color: #4051B5; text-decoration: none; font-size: 16px;">Python</a>
    <p style="margin: 5px 0 0 0; color: #666; font-size: 14px;">强大的编程语言，易学易用</p>
  </div>
  
  <div style="padding: 15px; border: 1px solid #e0e0e0; border-radius: 8px;">
    <a href="https://git-scm.com" style="font-weight: 600; color: #4051B5; text-decoration: none; font-size: 16px;">Git</a>
    <p style="margin: 5px 0 0 0; color: #666; font-size: 14px;">分布式版本控制系统</p>
  </div>
</div>
```

效果：

<div style="margin: 20px 0;">
  <div style="padding: 15px; border: 1px solid #e0e0e0; border-radius: 8px; margin-bottom: 10px;">
    <a href="https://zensical.org" style="font-weight: 600; color: #4051B5; text-decoration: none; font-size: 16px;">Zensical</a>
    <p style="margin: 5px 0 0 0; color: #666; font-size: 14px;">技术文档生成工具，简单高效</p>
  </div>
  
  <div style="padding: 15px; border: 1px solid #e0e0e0; border-radius: 8px; margin-bottom: 10px;">
    <a href="https://www.python.org" style="font-weight: 600; color: #4051B5; text-decoration: none; font-size: 16px;">Python</a>
    <p style="margin: 5px 0 0 0; color: #666; font-size: 14px;">强大的编程语言，易学易用</p>
  </div>
  
  <div style="padding: 15px; border: 1px solid #e0e0e0; border-radius: 8px;">
    <a href="https://git-scm.com" style="font-weight: 600; color: #4051B5; text-decoration: none; font-size: 16px;">Git</a>
    <p style="margin: 5px 0 0 0; color: #666; font-size: 14px;">分布式版本控制系统</p>
  </div>
</div>

---

## 徽章式链接

```html
<div style="display: flex; gap: 8px; flex-wrap: wrap; margin: 20px 0;">
  <a href="https://github.com" style="display: inline-block; padding: 5px 12px; background-color: #f0f0f0; color: #333; text-decoration: none; border-radius: 12px; font-size: 13px; font-weight: 500;">
    #GitHub
  </a>
  <a href="https://www.python.org" style="display: inline-block; padding: 5px 12px; background-color: #f0f0f0; color: #333; text-decoration: none; border-radius: 12px; font-size: 13px; font-weight: 500;">
    #Python
  </a>
  <a href="https://developer.mozilla.org" style="display: inline-block; padding: 5px 12px; background-color: #f0f0f0; color: #333; text-decoration: none; border-radius: 12px; font-size: 13px; font-weight: 500;">
    #MDN
  </a>
  <a href="https://stackoverflow.com" style="display: inline-block; padding: 5px 12px; background-color: #f0f0f0; color: #333; text-decoration: none; border-radius: 12px; font-size: 13px; font-weight: 500;">
    #StackOverflow
  </a>
</div>
```

效果：

<div style="display: flex; gap: 8px; flex-wrap: wrap; margin: 20px 0;">
  <a href="https://github.com" style="display: inline-block; padding: 5px 12px; background-color: #f0f0f0; color: #333; text-decoration: none; border-radius: 12px; font-size: 13px; font-weight: 500;">
    #GitHub
  </a>
  <a href="https://www.python.org" style="display: inline-block; padding: 5px 12px; background-color: #f0f0f0; color: #333; text-decoration: none; border-radius: 12px; font-size: 13px; font-weight: 500;">
    #Python
  </a>
  <a href="https://developer.mozilla.org" style="display: inline-block; padding: 5px 12px; background-color: #f0f0f0; color: #333; text-decoration: none; border-radius: 12px; font-size: 13px; font-weight: 500;">
    #MDN
  </a>
  <a href="https://stackoverflow.com" style="display: inline-block; padding: 5px 12px; background-color: #f0f0f0; color: #333; text-decoration: none; border-radius: 12px; font-size: 13px; font-weight: 500;">
    #StackOverflow
  </a>
</div>

---

## 脚注式链接

可以在文章中使用脚注引用外部链接[^1]。这种方式适合学术性文档[^2]。

```markdown
可以在文章中使用脚注引用外部链接[^1]。这种方式适合学术性文档[^2]。

[^1]: [Zensical 官方文档](https://zensical.org)
[^2]: [Python 官方文档](https://docs.python.org)
```

[^1]: [Zensical 官方文档](https://zensical.org)
[^2]: [Python 官方文档](https://docs.python.org)

---

## 下载链接样式

```html
<a href="https://www.python.org/downloads/" style="display: inline-flex; align-items: center; gap: 10px; padding: 12px 24px; background-color: #28a745; color: white; text-decoration: none; border-radius: 8px; font-weight: 500; font-size: 16px;">
  <span style="font-size: 24px;">⬇️</span>
  <span>下载 Python</span>
</a>
```

效果：

<a href="https://www.python.org/downloads/" style="display: inline-flex; align-items: center; gap: 10px; padding: 12px 24px; background-color: #28a745; color: white; text-decoration: none; border-radius: 8px; font-weight: 500; font-size: 16px;">
  <span style="font-size: 24px;">⬇️</span>
  <span>下载 Python</span>
</a>

---

## 高亮链接框

```html
<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 30px; border-radius: 12px; text-align: center; margin: 20px 0;">
  <h3 style="color: white; margin: 0 0 15px 0;">🚀 开始使用 Zensical</h3>
  <p style="color: rgba(255,255,255,0.9); margin: 0 0 20px 0;">快速构建美观的技术文档</p>
  <a href="https://zensical.org" style="display: inline-block; padding: 12px 30px; background-color: white; color: #667eea; text-decoration: none; border-radius: 8px; font-weight: 600;">
    访问官网
  </a>
</div>
```

效果：

<div style="background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); padding: 30px; border-radius: 12px; text-align: center; margin: 20px 0;">
  <h3 style="color: white; margin: 0 0 15px 0;">🚀 开始使用 Zensical</h3>
  <p style="color: rgba(255,255,255,0.9); margin: 0 0 20px 0;">快速构建美观的技术文档</p>
  <a href="https://zensical.org" style="display: inline-block; padding: 12px 30px; background-color: white; color: #667eea; text-decoration: none; border-radius: 8px; font-weight: 600;">
    访问官网
  </a>
</div>

---

## 总结

本页面展示了在 Zensical 文档系统中创建和美化外链的各种方法，包括：

- ✅ 基本 Markdown 链接语法
- ✅ 参考式和脚注式链接
- ✅ 按钮样式链接（实心、轮廓）
- ✅ 卡片式链接（基础、网格、渐变）
- ✅ 图标链接和社交媒体链接
- ✅ Admonition 和 Tabs 组合
- ✅ 链接列表（简洁、带描述）
- ✅ 徽章式链接
- ✅ 下载按钮
- ✅ 高亮展示框

选择合适的样式可以让您的文档更加美观和易用，主人。

---

<div style="text-align: center; margin-top: 50px; padding: 20px; background-color: #f5f5f5; border-radius: 8px;">
    <p style="font-size: 14px; color: #666;">
        📝 链接展示方法示例<br>
        🔗 包含所有常用链接样式和装饰
    </p>
</div>
