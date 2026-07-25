# DIKWP‑MESH 5.4 Ω PARALLAX UPLIFT

## 人类理解能力提升与证据运行系统 1.0.0  
## Human Understanding Capability Amplification & Evidence Runtime

> **不是“智力评分器”，而是一套把理解训练转换为可检验、可迁移、可延迟复测、可撤销且可审计证据的运行系统。**

UPLIFT 将附件中的 **PARALLAX CLOSURE MVP** 从“认知闭环结构诊断”升级为一个面向真实学习循环的 DIKWP‑MESH 5.4 Ω 运行时。它保留 PARALLAX 的观察者翻转、尺度扫描、规则对象化、目标悬置、模态注入、权力重分配和未知轴，同时补齐：

- 自愿、可撤销的理解契约；
- 训练前诊断与信心预测；
- 十二维理解证据画像；
- 检索、反事实、类比迁移、边界反例、观点旋转、尺度切换、未知保留与错误修订；
- 训练题、未见迁移题和延迟保持题的严格分离；
- 人工开放题的签名量表复核；
- scoped intervention lease；
- `response + score receipt + profile + event` 的 Ω 原子提交；
- nonce 幂等、崩溃回滚、Ed25519 回执、哈希链、Merkle checkpoint 和篡改检测；
- 本地认证 API 与单文件浏览器工作台；
- JSON Schema、测试、conformance、SBOM 和发行自证明。

---

## 1. 系统不是在优化什么

UPLIFT 明确拒绝以下用途：

- IQ、人格、心理健康或“认知等级”推断；
- 招生、就业、保险、信贷、执法或政治定向；
- 隐蔽说服、价值替换或绕过学习者否决权；
- 以训练题熟练度冒充迁移能力；
- 以一次迁移成功冒充长期保持；
- 以关键词命中冒充开放解释中的真正理解。

系统只对**特定知识包、特定任务、特定表单、特定时间与特定证据链**作范围受限的判断。

---

## 2. “理解”如何表示

UPLIFT 不输出一个总分，而维护十二维证据向量：

| 维度 | 核心问题 |
|---|---|
| Reconstruction | 能否脱离原文重建对象、关系和约束？ |
| Mechanism | 能否解释为什么以及通过什么路径发生？ |
| Prediction | 能否在新输入下生成可校验预测？ |
| Counterfactual | 能否说明干预、删边或反转条件后的变化？ |
| Transfer | 能否把结构迁移到未见领域，而非只复述表面词汇？ |
| Boundary | 能否识别适用范围、反例和边界外代价？ |
| Perspective | 能否切换观察者、尺度和利益相关方图册？ |
| Calibration | 作答前信心与实际表现是否匹配？ |
| Revision | 新证据出现时能否修订模型并保留原始痕迹？ |
| Compression | 能否用较短表达保留关键因果结构？ |
| Residual | 能否承认观测不足并保留 UAX 未知残差？ |
| Purpose | 能否说明模型服务谁、优化什么、牺牲什么以及否决条件？ |

每个维度只会进入以下证据状态之一：

```text
UNOBSERVED
  → EMERGING
  → PROVISIONAL
  → TRANSFER_SUPPORTED
  → RETENTION_SUPPORTED
```

**训练题表现永远不能直接生成 `TRANSFER_SUPPORTED`。** 只有预先隔离的未见表单可以支持迁移；只有真实延迟复测可以支持保持。

---

## 3. UPLIFT 的理解证明闭环

```text
知识包 + 私有评分键
        │
        ▼
PARALLAX 课程闭环审计
        │  observer / source / scale / modality / residual / purpose
        ▼
学习者 Intent Field Covenant
        │  purpose / domain / veto / prohibited outcomes / time budget
        ▼
基线任务 + 作答前信心
        │
        ▼
十二维画像 + 局部闭环诊断
        │
        ▼
瓶颈 → 最小可逆干预 → scoped leases
        │
        ├─ 检索与间隔复现
        ├─ 因果模拟与反事实
        ├─ 类比迁移与对比案例
        ├─ 观察者/尺度/模态切换
        ├─ 反例、边界与未知保留
        └─ 错误修订、teach-back、目的再契约
        │
        ▼
未见表单迁移门
        │
        ▼
延迟保持门
        │
        ▼
下一轮证据计划或开放义务
```

---

## 4. Ω 原子不变量

一次回答的关键状态在同一个 SQLite 事务中提交：

```text
COMMIT(
    response
  + durable nonce
  + intervention lease use
  + score result
  + multidimensional profile snapshot
  + hash-chained evidence event
  + Ed25519 signed receipt
)
OR COMMIT NOTHING
```

因此系统禁止：

- 回执返回但回答未落盘；
- nonce 已消费但评分或画像缺失；
- 租约已扣减但证据事件不存在；
- 进程重启后同一请求被重复执行；
- 同一 nonce 被不同回答双花；
- WAL 数据未纳入取证备份。

开放解释题的人工复核采用另一个不可变事务：

```text
COMMIT(
    signed rubric attestation
  + reviewed score overlay
  + new profile snapshot
  + evidence event
)
OR COMMIT NOTHING
```

原始待复核回执不会被改写。

---

## 5. 快速运行

### 5.1 从源码运行完整演示

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -e .

uplift54 demo \
  --example-dir examples/feedback_loops \
  --out outputs/demo

uplift54 conformance \
  --example-dir examples/feedback_loops \
  --out outputs/conformance

uplift54 artifacts-validate \
  --root . \
  --out outputs/ARTIFACT_VALIDATION.json

pytest -q
```

打开：

```text
outputs/demo/dashboard.html
```

### 5.2 启动本地学习工作台

先创建本地密钥种子和 API token。不要把真实密钥写入命令历史：

```bash
printf '%s' 'replace-with-a-long-random-local-seed' > .uplift-seed
python - <<'PY'
from secrets import token_urlsafe
print(token_urlsafe(32))
PY
```

把生成的 token 保存为 `.uplift-token`，然后：

```bash
uplift54 serve \
  --db local/uplift.sqlite \
  --pack examples/feedback_loops/knowledge_pack.json \
  --key examples/feedback_loops/scoring_key.private.json \
  --covenant examples/feedback_loops/understanding_covenant.json \
  --seed-file .uplift-seed \
  --token-file .uplift-token \
  --host 127.0.0.1 \
  --port 8765
```

浏览器打开：

```text
http://127.0.0.1:8765/studio
```

默认只绑定 loopback。该参考 API 不替代 TLS、OIDC、反向代理、细粒度授权或多租户隔离。

---

## 6. CLI

```text
uplift54 audit-pack          校验知识包并运行 PARALLAX 课程闭环审计
uplift54 register            注册知识包和私有评分键哈希
uplift54 activate-covenant   激活学习者控制的理解契约
uplift54 revoke-covenant     撤销契约并撤销所有活跃干预租约
uplift54 session             创建 baseline/training/transfer/delayed 会话
uplift54 submit              原子提交回答、评分、画像和签名回执
uplift54 review              追加开放解释题的签名量表复核
uplift54 plan                编译下一轮干预计划和 scoped leases
uplift54 profile             读取最新十二维理解证据画像
uplift54 status              查看持久状态计数和事件头
uplift54 verify              验证 SQLite、哈希、签名、nonce、租约和 checkpoint
uplift54 checkpoint          签发 Merkle 透明度 checkpoint
uplift54 serve               启动本地认证 API 与学习工作台
uplift54 demo                运行四阶段合成生命周期
uplift54 conformance         运行自包含一致性检查
uplift54 artifacts-validate  校验 Schema 与发行样例
```

---

## 7. 参考知识包

`examples/feedback_loops/` 提供“反馈回路与代理指标治理”双语知识包：

- 16 个概念；
- 40 个任务；
- baseline / training / transfer / delayed 四个严格分离阶段；
- 12 个理解维度；
- 5 个 DIKWP 资源层；
- 多观察者、尺度、模态和领域；
- 课程闭环审计；
- 私有评分键；
- 自愿理解契约；
- 合成响应轨迹。

发行包中的 `scoring_key.private.json` 是**公开的合成演示密钥**，只用于复现软件生命周期；它不能支持任何真实隐藏评估。对真实研究，必须另外生成未公开的评分键和迁移/延迟表单，并在训练阶段对学习者、生成模型和训练执行者隔离。运行时 API 仍只在服务端读取密钥，不通过 catalog 下发。

---

## 8. 当前参考结果

确定性合成演示产生：

- 4 个阶段会话；
- 39 个回答和签名回执；
- 4 个独立的人工量表式复核对象；
- 4 个适应性计划；
- 33 个 scoped intervention leases；
- 53 个哈希链证据事件；
- 1 个 Ed25519 签名 Merkle checkpoint；
- 12 个理解维度均被观测；
- 11 个维度获得合成迁移或延迟证据支持；
- 幂等重放、nonce 冲突、三个崩溃注入点、租约越界、账本篡改和 WAL 一致性备份均通过。

这些数字只说明**参考实现按设计运行**。合成答案和合成量表复核不代表真实学习者获得了同等提升。

---

## 9. 验证边界

本版本证据等级：

```text
E2 — author-side deterministic reference implementation
```

它已经验证：

- 软件状态机；
- 评分函数；
- 训练/迁移/延迟证据隔离；
- 原子提交与崩溃恢复；
- 签名、哈希链、Merkle root 与篡改检测；
- 知识包闭环审计；
- 干预租约和学习者契约；
- API 认证与评分键不公开；
- Schema、CLI、wheel 和离线 dashboard。

它尚未验证：

- 真实人群中的平均学习增益；
- 不同年龄、语言、学科、文化和可访问性需求下的公平性；
- 干预的因果效应大小；
- 长期依从性和真实延迟保持；
- 独立机构复现；
- 临床、就业、招生或其他高风险用途；
- 分布式共识、Byzantine fault tolerance 或生产多租户安全。

真正的有效性必须通过预注册、隐藏迁移表单、真实延迟复测、适当对照组、退出权与独立审计获得。参见 `docs/EVALUATION_PROTOCOL_CN_EN.md`。

---

## 10. 目录

```text
src/dikwp_mesh54_uplift/   核心运行时、API、CLI、报告与验证器
examples/feedback_loops/   参考知识包、私有评分键、契约和合成响应
schemas/                   16 个 JSON Schema
outputs/demo/              四阶段参考生命周期与离线 dashboard
outputs/conformance/       自包含一致性报告
outputs/                   制品验证和发行报告
dashboard/                 发行入口 dashboard
docs/                      架构、方法、研究、威胁模型、运维和评估协议
tests/                     单元、集成、安全、API、崩溃和制品测试
provenance/                附件来源哈希与升级说明
```

---

## 11. 进一步阅读

- `docs/BASELINE_AUDIT_CN_EN.md`
- `docs/ARCHITECTURE_CN_EN.md`
- `docs/METHOD_CN_EN.md`
- `docs/MESH54_OMEGA_MAPPING_CN_EN.md`
- `docs/LEARNER_GUIDE_CN.md`
- `docs/AUTHORING_GUIDE_CN_EN.md`
- `docs/API_REFERENCE_CN_EN.md`
- `docs/THREAT_MODEL_CN_EN.md`
- `docs/SCIENTIFIC_BOUNDARY_CN_EN.md`
- `docs/EVALUATION_PROTOCOL_CN_EN.md`
- `docs/OPERATIONS_RUNBOOK_CN_EN.md`
- `docs/RESEARCH_BASIS_CN_EN.md`
- `SECURITY.md`
- `GOVERNANCE.md`

---

## 12. License

Apache License 2.0。附件中的 PARALLAX CLOSURE MVP 作为输入基线，其原许可与来源哈希保留在 `provenance/`。
