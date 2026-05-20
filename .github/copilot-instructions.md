# 项目指导

## 项目概述

- **项目名**: @fygame/tsnode
- **类型**: ESM (ECMAScript Module) Node.js 包
- **描述**: TypeScript 结合 Node.js 的测试项目
- **作者**: Sundy
- **入口点**: `lib/index.js` → `src/index.ts`

## 代码风格

- **语言**: TypeScript 5.6.2
- **模块系统**: ESM (NodeNext)
- **目标版本**: ESNext
- **编译配置**: 
  - 源目录: `src/`
  - 输出目录: `lib/`
  - 启用 Source Map

## 架构与结构

项目采用简单的 TypeScript → JavaScript 编译结构：

- **源代码**: `src/` 目录中的 TypeScript 文件
- **编译输出**: `lib/` 目录（自动生成，无需手动编辑）

### 重要特性

- ESM 模块模式 (`"type": "module"` in package.json)
- Source Map 支持便于调试编译后的代码

## 构建与测试

### 常用命令

| 命令 | 用途 | 说明 |
|------|------|------|
| `npm run build` | 开发模式编译 | `tsc --watch` 监视源文件变化自动重编 |
| `npm run build:ci` | CI 编译 | 一次性编译，生成 `lib/` 目录 |
| `npm start` / `npm test` | 运行程序 | 使用 `node --watch` 监视 `lib/index.js`，传入参数 "sundy"，加载 `.env` |

### 运行流程

```bash
# 1. 编译 (watch 模式)
npm run build

# 2. 在另一个终端运行 (包含热重载)
npm start
```

### 特殊配置

- **CLI 参数**: 程序启动时自动传入 `"sundy"` 参数
- **环境变量**: 通过 `--env-file=.env` 加载
- **监视模式**: Node.js 原生 `--watch` (需 Node.js 20.6+)
- **平台特定**: 使用 `cls` 清屏（Windows 环保）

## 项目约定

### 非标准模式

1. **运行参数**: 每次运行固定传入 "sundy" 参数（作者标记或测试值）

### 依赖项特点

- **作用域包**: `@fygame/wait`, `fy-convertor`, `@taiyosen/easy-svn`（私有依赖）
- **开发工具**: ts-morph (AST 操作), commander (CLI)
- **运行时**: axios, chalk, express, dotenv, concurrently

## AI 开发建议

- 修改源代码时编辑 `src/` 中的 `.ts` 文件，不要直接编辑 `lib/` 
- 新增模块时按 ESM 风格使用 `export` / `import`
- 调试时参考生成的 Source Map (`.js.map`) 文件
- 本地开发使用 `npm run build` + `npm start` 组合实现热重载
