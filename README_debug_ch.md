# 调试工作流详细指南 | Debug Workflow Detailed Guide

> 🌍 **Language Version | 语言版本**: [English Version](README_debug_en.md) | [返回主页](README.md)

## 📋 目录

- [概述](#概述)
- [工作流特点](#工作流特点)
- [使用方法](#使用方法)
- [6步调试循环](#6步调试循环)
- [环境设置](#环境设置)
- [模板使用](#模板使用)
- [符号系统](#符号系统)
- [最佳实践](#最佳实践)
- [常见问题](#常见问题)

## 概述

调试工作流是一个基于GitHub Copilot的系统化调试解决方案，专为AI辅助开发设计。它提供了结构化的问题解决方法，确保调试过程的一致性和效率。

### 核心模板
- **主模板**: `debug-system/debug_workflow_template.md`
- **支持文件**: `debug-system/` 目录下的所有模板和工具

## 工作流特点

### 🎯 系统化调试流程
- **6步调试循环**: 问题识别 → 分析 → 假设 → 验证 → 修复 → 总结
- **结构化文档**: 每个调试会话都有完整的文档记录
- **版本管理**: 多轮调试的版本控制和历史追踪

### 🤖 AI协作优化
- **Copilot集成**: 专为GitHub Copilot Agent模式优化
- **自然语言交互**: 用自然语言描述问题，AI自动解析
- **智能建议**: AI基于上下文提供调试建议

### 📊 文件组织系统
- **符号分类**: 使用表情符号进行直观的文件分类
- **分层存储**: core/archive/deprecated等多层级文件管理
- **快速导航**: 清晰的目录结构和索引系统

## 使用方法

### 步骤1: 初始化调试环境

```powershell
# 创建调试目录
mkdir debug
cd debug

# 设置轮次变量
$round = 1

# 创建标准目录结构
mkdir $round\{src,core,archive,deprecated,docs,logs,files}

# 复制README模板
Copy-Item "..\debug-system\templates\README-template.md" "$round\README.md"
```

### 步骤2: 复制工作流模板

```powershell
# 为特定任务复制模板到debug-system目录
Copy-Item "debug-system/debug_workflow_template.md" "debug-system/debug_workflow_[任务名称].md"
```

### 步骤3: 在VS Code中启动

```powershell
# 打开工作流文档
code debug_workflow_[任务名称].md

# 确保Copilot Agent模式已启用
# 使用 @workspace 命令开始会话
```

### 步骤4: 配置自动触发（可选）

您可以在项目根目录创建`.copilot-instructions.md`文件来启用自动工作流触发：

```markdown
# Copilot调试工作流指令

## 自动触发条件
当用户提到：调试、错误修复、故障排除、bug解决、代码问题时
自动建议："我注意到您在进行调试工作。是否需要我启动系统化调试工作流？我可以创建结构化的调试会话文档来帮助组织故障排除过程。"

## 工作流模板
- 调试模板: `debug-system/debug_workflow_template.md`
```

**选择您的方式**:
- **自动触发**: 配置`.copilot-instructions.md`实现无缝工作流激活
- **手动触发**: 手动打开工作流模板文档

### 步骤5: 描述问题并开始调试

1. **问题描述**: 用自然语言详细描述你遇到的问题
2. **AI分析**: Copilot会分析问题并提出调试计划
3. **确认理解**: 确认AI对问题的理解是否正确
4. **开始调试**: 按照6步调试循环执行

## 6步调试循环

### 1. 🔍 问题识别 (Problem Identification)
- 明确定义问题现象
- 收集错误信息和日志
- 确定问题的影响范围

### 2. 📊 问题分析 (Analysis)
- 分析问题的根本原因
- 检查相关代码和配置
- 查看系统环境和依赖

### 3. 💡 假设形成 (Hypothesis)
- 基于分析提出可能的原因
- 制定验证计划
- 设定优先级

### 4. 🧪 假设验证 (Verification)
- 设计和执行测试
- 收集验证数据
- 记录测试结果

### 5. 🔧 问题修复 (Fix)
- 实施解决方案
- 进行回归测试
- 验证修复效果

### 6. 📝 总结记录 (Summary)
- 记录解决过程
- 更新文档
- 总结经验教训

## 环境设置

### 目录结构说明

```
debug/
└── 1/                          # 第一轮调试
    ├── src/         🐍         # 工作代码目录
    ├── core/        🔴         # 核心解决方案 (5-10个关键文件)
    ├── archive/     📚         # 重要里程碑文件
    ├── deprecated/  🗑️         # 废弃文件
    ├── docs/        📝         # 分析文档
    ├── logs/        📋         # 测试日志
    ├── files/       🗂️         # 其他支持文件
    └── README.md               # 调试会话文档
```

### 符号系统

| 符号 | 目录 | 用途 | 存储规则 |
|------|------|------|----------|
| 🐍 | src/ | 当前工作代码 | 调试过程中的所有代码文件 |
| 🔴 | core/ | 核心解决方案 | 最多保留5-10个关键文件 |
| 📚 | archive/ | 重要里程碑 | 阶段性成果和重要版本 |
| 🗑️ | deprecated/ | 废弃文件 | 无效或被替代的文件 |
| 📝 | docs/ | 分析文档 | 问题分析和解决方案文档 |
| 📋 | logs/ | 测试日志 | 调试过程中的日志记录 |
| 🗂️ | files/ | 支持文件 | 其他辅助文件 |

## 模板使用

### README模板 (README-template.md)
用于记录每个调试会话的详细信息，包括：
- 问题描述
- 调试过程
- 解决方案
- 经验总结

### 总结模板 (summary-template.md)
用于项目级别的总结报告，包括：
- 整体问题概述
- 解决方案汇总
- 性能影响分析
- 后续建议

### 经验模板 (experience-template.md)
用于记录调试过程中的经验教训：
- 成功的调试方法
- 遇到的陷阱
- 最佳实践
- 工具推荐

## 最佳实践

### Copilot配置建议

#### 模型选择
- **推荐模型**: Claude 4.0
- **备选模型**: GPT-4 或其他高级模型
- **避免使用**: 基础模型（可能影响调试质量）

#### 会话设置
- **预算控制**: 每次会话10-20个请求
- **思考模式**: 开启AI思考模式
- **终端权限**: 确保有终端访问权限

### 调试策略

#### 问题描述
- **具体详细**: 提供具体的错误信息和复现步骤
- **环境信息**: 包含系统环境、版本信息等
- **期望结果**: 明确说明期望的正确行为

#### 验证方法
- **小步验证**: 将复杂问题分解为小步骤验证
- **回归测试**: 每次修改后进行全面测试
- **文档记录**: 详细记录每个验证步骤和结果

### 文件管理

#### 版本控制
- **定期归档**: 将重要阶段性成果移入archive目录
- **清理废弃**: 及时清理deprecated目录中的过期文件
- **核心精简**: 保持core目录文件数量在5-10个以内

#### 文档同步
- **实时更新**: 调试过程中实时更新README文档
- **交叉引用**: 在文档中添加相关文件的引用链接
- **总结归纳**: 每轮调试结束后进行总结

## 常见问题

### Q: AI偏离调试主题怎么办？
**A**: 立即暂停并重新描述问题。如果预算接近用完，考虑重新开始会话。

### Q: 调试过程中文件太多怎么管理？
**A**: 严格按照符号系统分类，定期清理deprecated目录，将重要文件移入core或archive。

### Q: 如何记录复杂的调试过程？
**A**: 使用层次化的文档结构，为每个主要步骤创建单独的文档文件，在主README中建立索引。

### Q: 多轮调试如何管理？
**A**: 为每轮调试创建独立的数字目录（1/、2/、3/等），在根目录README中维护轮次索引。

### Q: 如何与团队共享调试结果？
**A**: 使用summary模板创建项目级总结，将关键文件整理到core目录，编写清晰的文档说明。

---

**最后更新**: 2025年6月24日  
**版本**: v2.1  
**维护者**: Copilot Workflow System Team
