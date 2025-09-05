# 为 AI 编程助手准备的 Irys 文档

[English](./README.md)

## 这是什么？

这个仓库下载了 Irys 的全部官方文档，并将其处理成专为 AI 编程助手（例如 "vibe coder"）使用的上下文文件。

其主要目标是为 AI 工具提供一个关于 Irys SDK 及其功能的全面且最新的知识库。

如需查看详细的开发者指南，请参考：[Irys Web3 开发者指南](./Irys-Web3开发者指南.md)

## 生成的文件

该流程会生成两个主要文件：

- **`LLM_Full.txt`**: 包含完整、拼接在一起的所有文档。这是为 AI 提供最完整上下文的理想选择。
- **`LLM_Simple.txt`**: 一个更简洁的文档摘要版本，适用于快速参考或在有 token 限制时的场景。

## 如何使用

您可以复制 `LLM_Simple.txt` 或 `LLM_Full.txt` 的内容，并将其作为上下文提供给您的 AI 编程助手。这将使其能够为 Irys 相关的开发任务生成更准确、更具上下文感知能力的代码。

## 来源

所有文档均源自 Irys 官方文档网站：https://docs.irys.xyz/

## 在 AI 工具中使用

### 在 Cursor 中使用

**添加上下文文件:**

将 `LLM_Full.txt` 或 `LLM_Simple.txt` 放入您的项目文件夹（例如，根目录或 `docs/`）。

**与 @Docs 集成:**

1. 在 Cursor 中，打开 Composer (`Ctrl+Shift+I` 或 `Cmd+Shift+I`) 并输入 `@Docs`。
2. 选择“添加新文档”(Add new doc)并提供 `LLM_Full.txt` 或 `LLM_Simple.txt` 的文件路径或 URL。
3. Cursor 会索引该文件以便在提示中使用。

**提示示例:**

> 创建一个使用 Irys 上传简单字符串的脚本，遵循 `@Docs LLM_Full.txt` 获取详细指南或 `LLM_Simple.txt` 进行最小化设置。

**技巧:**

- 对于复杂的 Irys 配置，请使用 `LLM_Full.txt`；对于基本上传，请使用 `LLM_Simple.txt`。
- 保持文件内容清晰，以适应 Cursor 的上下文限制。

### 在 Claude Code 中使用

**创建 CLAUDE.md:**

1. 在您的项目根目录或父/子目录中创建一个 `CLAUDE.md` 文件。
2. 将 `LLM_Full.txt` 或 `LLM_Simple.txt` 的内容复制到 `CLAUDE.md` 中。这是 Claude Code 自动提取上下文的标准方式。

**运行 Claude Code:**

- 使用 CLI: `claude --file CLAUDE.md` 来加载上下文。
- 或者，如果使用图形界面，直接将 `CLAUDE.md` 的内容粘贴到提示中。

**提示示例:**

> 根据 `CLAUDE.md` 中的上下文（基于 `LLM_Full.txt` 的详细规格或 `LLM_Simple.txt` 的最小化设置），创建一个使用 Irys 上传简单字符串的脚本。

**技巧:**

- 如果支持，使用 `/init` 自动生成包含项目上下文的 `CLAUDE.md`。
- 为快速进行 Irys 上传，请确保 `CLAUDE.md` 包含 `LLM_Simple.txt` 的内容以最小化 token 使用量。
- 如果 Claude Code 需要获取外部的 `llms.txt` URL，请批准其工具调用。