# Irys Documentation for AI Coding Assistants

[中文](./README.zh-cn.md)

## What is this?

This repository downloads the complete official documentation for Irys and processes it into context files specifically for use with AI coding assistants, such as "vibe coder".

The primary goal is to provide AI tools with a comprehensive and up-to-date knowledge base of the Irys SDK and its functionalities.

## Generated Files

This process generates two main files:

- **`LLM_Full.txt`**: Contains the complete, concatenated documentation. This is ideal for providing the AI with maximum context.
- **`LLM_Simple.txt`**: A more concise, summarized version of the documentation, suitable for quick reference or when token limits are a concern.

## Usage

To use this, you can copy the content of either `LLM_Simple.txt` or `LLM_Full.txt` and provide it as context to your AI coding assistant. This will enable it to generate more accurate and context-aware code for Irys-related development tasks.

## Source

All documentation is sourced from the official Irys documentation website: https://docs.irys.xyz/

## Using with AI Tools

### Using with Cursor

**Add Context Files:**

Place `LLM_Full.txt` or `LLM_Simple.txt` in your project folder (e.g., root or `docs/`).

**Integrate with @Docs:**

1. In Cursor, open Composer (`Ctrl+Shift+I` or `Cmd+Shift+I`) and type `@Docs`.
2. Select "Add new doc" and provide the file path or URL to `LLM_Full.txt` or `LLM_Simple.txt`.
3. Cursor indexes the file for use in prompts.

**Prompt Example:**

> Create a script that uses Irys to upload a simple string, following `@Docs LLM_Full.txt` for detailed guidelines or `LLM_Simple.txt` for a minimal setup.

**Tips:**

- Use `LLM_Full.txt` for complex Irys configurations, `LLM_Simple.txt` for basic uploads.
- Keep files clear to fit Cursor’s context limits.

### Using with Claude Code

**Create CLAUDE.md:**

1. Create a `CLAUDE.md` file in your project root or a parent/child directory.
2. Copy the content of `LLM_Full.txt` or `LLM_Simple.txt` into `CLAUDE.md`. This is the standard way for Claude Code to automatically ingest context.

**Run Claude Code:**

- Use the CLI: `claude --file CLAUDE.md` to load the context.
- Alternatively, paste `CLAUDE.md` content directly into the prompt if using an interface.

**Prompt Example:**

> Create a script that uses Irys to upload a simple string, following the context in `CLAUDE.md` (based on `LLM_Full.txt` for detailed specs or `LLM_Simple.txt` for a minimal setup).

**Tips:**

- Use `/init` to auto-generate `CLAUDE.md` with project context if supported.
- For quick Irys uploads, ensure `CLAUDE.md` contains `LLM_Simple.txt` content to minimize token usage.
- Approve tool calls if Claude Code fetches external `llms.txt` URLs.