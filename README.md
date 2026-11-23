# SalesHire Fit Navigator — 循证销售招聘决策与场景压力测试系统

> **在线交互原型 (Live Demo)**：[点击体验在线系统](https://frank-hy.github.io/SalesHire-Fit-Navigator/)  
> **项目定位**：面向销售负责人与招聘经理的**数据与实证驱动型（Evidence-Based）人才评估辅助决策工具**

---

## 1. 产品背景与痛点洞察 (Product Background & Pain Points)

在 B2B、大客户及高强度数字化销售团队的招聘与晋升中，业务负责人常因依赖直觉和经验主义陷入三大决策误区：

1. **唯垂直行业背景论**：过度看重候选人在窄众细分行业的过往履历，忽略了核心销售方法论（Sales Mastery）的跨行业可迁移性，导致错失高潜人才。
2. **销冠晋升陷阱（Peter Principle）**：默认“顶尖一线销售（Top Performer）= 优秀销售经理”，忽略了管理岗对团队辅导、内部社会资本（Internal Social Capital）与跨部门协同的差异化要求。
3. **静态评估表失真**：传统结构化面试打分表采用固定权重，无法根据外部市场竞争烈度、企业资源支持度以及 CRM/AI 工具渗透率进行动态校准。

**SalesHire Fit Navigator** 将国际顶尖商学院的三篇销售管理实证研究转化为**可交互的动态权重引擎与场景模拟器**，帮助决策者在复杂业务约束下量化评估候选人匹配度并提前规避用人风险。

---

## 2. 核心功能模块 (Core Features)

### ① 岗位画像与业务上下文配置 (Role & Operational Context Setup)
* **双轨岗位模型**：支持切换 **一线销售代表（Frontline Rep）** 与 **销售经理（Sales Manager）** 两套差异化底层评估基准。
* **招聘来源区分**：支持 **内部晋升（Internal Promotion）** 与 **外部社招（External Hire）** 模式切换，动态调整组织内部社会资本权重。
* **业务形态适配**：覆盖 B2B、B2C、大客户（Key Account）、外勤（Field Sales）与数字销售（Digital Sales）五大场景及品牌势能强弱配置。

### ② 多维胜任力评估矩阵 (12-Dimension Competency Assessment)
* 围绕**职业履历路径**、**动态销售效能**与**高压约束判断**三大维度，拆解为 **12 项量化评估指标**（1–5 分制交互打分），并实时计算评估完整度（Confidence Metrics）。

### ③ 实时场景压力测试器 (Scenario Pressure Testing Panel)
* 招聘经理可通过交互按钮实时模拟外部业务冲击（**市场竞争压力**、**公司资源支持度**、**CRM/AI 技术强度**）。
* 底层权重引擎基于学术实证规则实时重算各维度占比，右侧仪表盘同步刷新候选人匹配得分与录用建议等级（Strong Hire / Conditional Hire / Develop Before Hiring / Not Recommended）。

### ④ 循证风险预警与结构化面试生成 (Risk Warnings & Interview Protocol)
* **启发式风险诊断**：自动识别“高行业经验但低核心销售经验”、“高个人成交力但低团队辅导潜质”等典型招聘陷阱，并给出对应的文献级风险提示。
* **定制化面试题库与行动清单**：根据目标岗位短板与场景压力，自动生成针对性的行为面试问题（Structured Interview Questions）及下一步录用/培养建议（Next Steps）。

---

## 3. 学术依据与动态权重算法 (Evidence-Based Algorithm)

本系统的权重分配与动态调节机制严格映射以下三篇同行评审（Peer-Reviewed）学术文献的核心实证结论：

| 学术文献 | 核心实证结论 | 产品算法映射逻辑 |
| :--- | :--- | :--- |
| **Keshavarz et al. (2023)**<br>*How do firms value sales career paths?* | 通用销售经验具备高可迁移性；一线业绩不等于管理潜质；内部晋升高度依赖企业内部社会资本。 | 一线岗赋予通用销售经验（20%）高于单一行业经验（5%）的基准权重；管理岗侧重领导力（25%）与内部社会资本（20%），并触发防错配预警。 |
| **Claro et al. (2023)**<br>*Dynamic and global drivers of salesperson effectiveness* | 个体能力驱动力（技巧、天赋、适应力、内驱力）在强竞争、弱品牌或低资源环境下尤为关键。 | 当场景切换至**高市场竞争**或**低资源/弱品牌**时，系统自动上调销售技巧、适应力与内驱力的权重占比。 |
| **Lam & Borgh (2021)**<br>*On salesperson judgment and decision making* | 销售决策受制于 **3Cs 框架（Context 情境、Task 任务特征、Constraints 约束条件）**，技术变革与高压考验判断力。 | 当业务处于**高 CRM/AI 强度**、**高客户复杂度**或**高时间压力**时，显著提高技术就绪度与高压判断力的权重系数。 |

### 核心评分公式
系统在每次参数或评分变更时，执行权重动态偏移与归一化计算：

$$w'_i = \frac{w_i + \Delta w_i}{\sum_{j=1}^{n} (w_j + \Delta w_j)}$$

候选人最终匹配度得分 $S_{\text{fit}} \in [0, 100]$ 计算如下：

$$S_{\text{fit}} = \text{round}\left( \sum_{i=1}^{n} w'_i \cdot (20 \times r_i) \right)$$

其中 $w_i$ 为岗位基准权重，$\Delta w_i$ 为业务场景与外部压力触发的动态调整增量，$r_i \in \{1,2,3,4,5\}$ 为候选人在第 $i$ 项指标的评估得分。

---

## 4. 技术实现与架构说明 (Tech Stack)

* **前端框架**：React 18 + Tailwind CSS
* **架构特点**：采用单文件零构建架构（`index.html` 内置 Babel 运行时编译与 CDN 依赖），无需复杂脚手架即可在浏览器本地双击打开，或一键托管至 GitHub Pages / Netlify。
* **状态计算**：基于 React `useMemo` 构建响应式规则引擎，实现毫秒级权重重算与交互反馈。

---

## 5. 未来产品迭代规划 (Product Roadmap)

若将该原型进一步演进为企业级 **AI × HRTech** 产品，规划以下迭代方向：
1. **LLM 简历智能解析与预打分**：接入大语言模型解析候选人 PDF 简历与过往业绩描述，自动生成 12 项维度的初始推荐评分及置信度依据，降低面试官手动录入成本。
2. **AI 模拟面试官（Role-Play Agent）**：针对系统诊断出的低分短板维度，由 AI 扮演高难度客户进行多轮对话压力测试，自动评估候选人的临场适应力与高压判断力。
3. **历史入职绩效闭环校准**：打通企业 CRM 业绩数据，追踪已录用候选人入职 6–12 个月后的实际产出，持续反向微调权重参数 $\Delta w_i$。
