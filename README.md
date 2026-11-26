# DSH 插件索引 · 隐私防护插件集

DeepSeek Harness (DSH) 的插件索引（format 1），收录个人智能体隐私防护插件。

## 索引地址

```
https://kaitoukk.github.io/dsh-plugin-market/index.json
```

## 使用方法

1. 打开 DSH → **插件** → **实验性插件** → 打开 **自定义插件索引**
2. 在 **已安装** 旁的 **发现** 标签页点 **添加索引源**
3. 输入上面的索引 URL
4. 在「发现」中浏览并安装插件

> DSH 不内置索引源，需要手动添加。索引源属于当前 profile。

## 收录插件

### dsh-privacy-guard — 隐私防护

确定性隐私防护（零模型调用、低延迟）：
- **PII 检测与动态脱敏**：手机号 / 身份证 / 邮箱 / 银行卡 / API Key / JWT / 口令赋值
- **提示词注入检测**：中英文「忽略指令 / 角色接管 / 诱导泄密 / 数据外带」
- **敏感操作审批拦截**：`rm -rf` / 批量删除 / 覆盖源码 / 数据外发 / 读凭据 → `allow/ask/block`
- **审计日志**：内存或 JSONL 落盘，事件脱敏后记录

- 仓库：https://github.com/KaitouKK/dsh-privacy-guard
- 安装指引：[INSTALL.md](https://github.com/KaitouKK/dsh-privacy-guard/blob/main/INSTALL.md)

### dsh-privacychecker — 操作前隐私审查

在 Agent 关键操作**真正执行前**增加一道模型审查（方法移植自 [microsoft/ACV PrivacyInAction](https://github.com/microsoft/ACV/tree/main/misc/PrivacyInAction)）：
- 挂载 DSH 的 `tools/pre-execute`，输出 **ALLOW / MODIFY / BLOCK**
- 基于信息流分析 + 数据最小化原则判断「是否必要、可否披露、是否越界」
- 读类操作经 `tools/post-execute` 自动脱敏读回内容
- 用同一 Agent 模型执行审查，**无需独立推理服务**

- 仓库：https://github.com/KaitouKK/dsh-privacychecker
- 评估报告：https://github.com/KaitouKK/dsh-privacychecker/blob/main/eval/results/report.md

## 手动安装（不经市场）

```bash
git clone https://github.com/KaitouKK/dsh-privacy-guard.git
cp -r dsh-privacy-guard ~/.dsh/plugins/
# 在 ~/.dsh/profiles/web/cordis.patch.yml 中 insert 插件入口（见各仓库 INSTALL.md）
```

## 索引结构

```
.
├── index.json          # 索引（format 1，已通过官方 dsh-plugin-market-index 校验）
└── icons/
    ├── dsh-privacy-guard.svg
    └── dsh-privacychecker.svg
```

版本来源为 Git 仓库，已 pin 到具体 commit SHA，安装可复现。

## 许可

各插件均为 MIT。
