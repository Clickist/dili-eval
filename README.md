# DILI Eval - 尽调报告评估 Skill

Claude Code 技能，用于对投资尽职调查报告进行五维度质量评估和事实核查。

## 功能特点

- 📄 **多格式支持**：自动检测PDF/MD/TXT格式，PDF文件自动提取文本
- 📊 **五维度评估**：完整性、准确性、深度性、实用性、可读性
- 🔍 **Fact Check**：联网检索验证关键事实
- 📝 **对比评估**：支持单报告评估和两份报告对比评估

## 安装方法

### 方法一：直接下载

```bash
# 创建skill目录
mkdir -p ~/.claude/skills/dili-eval

# 下载文件（将此仓库克隆或下载后）
cp -r dili-eval/* ~/.claude/skills/dili-eval/
```

### 方法二：Git Clone

```bash
cd ~/.claude/skills
git clone https://github.com/Clickist/dili-eval.git
```

## 使用方法

### 单报告评估

```
/dili-eval 待分析报告/某公司尽调报告.pdf
```

输出：单份报告的质量评估 + Fact Check结果

### 对比评估

```
/dili-eval compare 待分析报告/报告A.pdf 待分析报告/报告B.pdf
```

输出：两份报告的对比评估报告

## 评估标准

### 七大核心章节

| 章节 | 权重 | 核心内容 |
|------|------|----------|
| 执行摘要 | 10% | 交易概述、关键发现、投资建议 |
| 公司基本情况 | 15% | 基本信息、历史沿革、股权结构 |
| 行业与竞争 | 15% | 行业概况、政策、竞争格局 |
| 业务与技术 | 20% | 主营业务、核心产品、技术研发 |
| 财务情况 | 20% | 财务报表、关键指标、盈利预测 |
| 投资价值分析 | 10% | 投资亮点、估值测算 |
| 风险与对策 | 10% | 行业风险、公司风险、财务风险 |

### 五维度评分

| 维度 | 权重 | 评分要点 |
|------|------|----------|
| 完整性 | 20% | 信息覆盖全面，无重大遗漏 |
| 准确性 | 25% | 数据准确，来源可靠 |
| 深度性 | 20% | 分析深入，有洞察 |
| 实用性 | 20% | 对决策有实质帮助 |
| 可读性 | 15% | 结构清晰，表述专业 |

### 评级标准

- **优秀**：总分≥90分，且各维度均≥良好
- **良好**：总分80-89分，且无不合格维度
- **合格**：总分60-79分，且无严重不合格维度
- **不合格**：总分<60分

## 依赖

- Python 3.x
- pdfplumber（用于PDF文本提取）

```bash
pip install pdfplumber
```

## 文件结构

```
dili-eval/
├── SKILL.md              # 主指令文件
├── README.md             # 说明文档
├── reference/
│   └── evaluation-standard.md   # 评估标准参考
└── examples/
    └── example-output.md        # 评估报告输出示例
```

## 联网检索工具

Skill 会询问用户使用的联网检索工具：
1. WebFetch/WebSearch（默认）- Claude Code内置
2. Firecrawl API - 需配置API密钥
3. 其他工具 - 自定义配置
4. 跳过Fact Check

## License

MIT License

## 版本

v1.0.0
