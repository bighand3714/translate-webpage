# translate-webpage

将网页内容（URL 或本地 HTML 文件）转化为干净的中文 Markdown 文档的 Claude Code skill。专为 Wiki 百科和访谈文档优化——完整保留图片链接和引用来源。

## 特性

- 支持单 URL / 多 URL 并行翻译 / 本地 HTML 文件
- 子 agent 并行架构：翻译由 `sonnet` 模型子 agent 执行，更快更省钱
- 逐句翻译，段落级别一一对应，不改写原文
- 完整保留图片、链接、表格、脚注、参考资料
- 可选双语对照输出（`--bilingual`）
- 自动生成 Obsidian 兼容的 frontmatter
- 支持通过文件传入 URL 列表（`@urls.txt`）或 IDE 选区

## 安装

```bash
# 克隆到 Claude Code skills 目录
git clone https://github.com/<your-username>/translate-webpage.git ~/.claude/skills/translate-webpage
```

或者直接复制 `SKILL.md` 到 `~/.claude/skills/translate-webpage/SKILL.md`。

Claude Code 会自动加载该目录下的 skill。

## 使用

```bash
# 单 URL
/translate-webpage https://en.wikipedia.org/wiki/The_Legend_of_Zelda

# 双语对照
/translate-webpage https://example.com/article --bilingual

# 指定输出子目录
/translate-webpage https://example.com/article --output games/

# 多 URL 并行
/translate-webpage https://en.wikipedia.org/wiki/Zelda https://en.wikipedia.org/wiki/Mario

# 从文件读取 URL 列表
/translate-webpage @urls.txt --bilingual

# 本地 HTML 文件
/translate-webpage "C:\Downloads\interview.html"
```

## 依赖

- **defuddle** CLI（推荐）：用于提取干净网页内容
  ```bash
  npm install -g defuddle
  ```
- 若 defuddle 不可用，自动回退到 WebFetch 工具

## 配置要求

子 agent 翻译需要 `sonnet` 模型可用。如果你将 sonnet 映射到 faster/cheaper 模型（如 DeepSeek），翻译速度和成本会进一步优化。

## 文件结构

```
translate-webpage/
├── README.md
├── SKILL.md          # skill 定义文件
├── .gitignore
└── LICENSE
```

## 许可

MIT
