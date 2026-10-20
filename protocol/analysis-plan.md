# 统计分析计划（Statistical Analysis Plan, SAP）

> 版本 `v1.0`　冻结日 **2026-10-18**　冻结人：小何
> 冻结后不得因看到结果而改动；任何改动追加到 §10 偏差记录，并注明改动日与理由。
> 本计划与 `criteria.txt`（PICOS v2）配套；纳入排除已完成，PRISMA 计数见 `output/prisma.md`。

## 1. 分析对象

- 纳入报告 **39** 篇 → 分析单位 **33 项研究**（`protocol/cohort_map.yaml`；同一队列多篇报告只算一项）。
- 双轨人群（仅用于亚组与敏感性，不改变主分析）：`main` 健康/规律运动者 28 项、`sens` 有共病但做运动 11 项。
- 结局域 **4 个**：睡眠、运动表现、氧化应激、炎症。判定口径见 `extraction/CONVENTIONS.md` §2。
- `R0170`（`10.1556/2060.2022.00126`）全文只有 2 页预览、拿不到任何结局数值 → **计入纳入但无数据**，进 PRISMA「数据缺失」，不参与任何合并，在正文与森林图中标注。

## 2. 效应量

### 2.1 主口径：域级标准化均数差（SMD）
- 每个域内所有结局**方向先统一**（见 §2.4），按 Hedges' g 标准化。
- 标准化分母用**两条件合并 SD**（`d_av` 口径）：
  `d = (m_MEL − m_PLA) / sd_pooled`，`sd_pooled = √((sd_MEL² + sd_PLA²)/2)`。
  理由：交叉与平行研究用同一分母定义才能同池；`d_av` 对两条件方差不等更稳健。
- 次级输出（不改主口径）：同一结局单位一致、可直接换算时同时报**均数差 MD**（如 CK、LDH、CRP 统一为 IU/L、mg/L）。

### 2.2 设计特异方差
| 设计 | 点估计 | 方差 |
|---|---|---|
| 平行（两臂独立） | `m_MEL − m_PLA` | `vi = sd_pooled² × (1/n_MEL + 1/n_PLA)`（SMD 尺度含小样本校正） |
| 交叉 / 自身前后对照 | 两条件均数差 | `SD_diff = √(sd_MEL² + sd_PLA² − 2·r·sd_MEL·sd_PLA)`；`vi = SD_diff² / n` |

**r（条件内相关系数）取值顺序**（永不静默取默认值，逐条在输出表里记 `r_source`）：
1. **反解**：同一研究同一结局若报告了配对 t / F / 配对 CI，直接反解 r；
2. **借用**：本综述内已有配对统计的研究的中位 r；
3. **默认 `r = 0.5`**（主分析），敏感性 `r = 0.2` / `r = 0.8`（小何 2026-10-18 裁定）。

### 2.3 缺均值 / 缺离散度
- **中位数 + IQR**（共 40 行，来自 `10.3390/nu18091425` 与 `10.3390/sports13060190`，原文只报 IQR 宽度、无法用 Wan 法）：
  按 `σ ≈ IQR宽度 / 1.349` 近似（逐条标记 `sigma_approx: iqr_range/1.349`），
  **只进入域级合并**，不进入任何单结局合并；并在敏感性分析里与排除这 40 行的结果对比。
- **图上取点**：均值进入主分析；图上误差棒因与柱顶/标记粘连、精度不足，**不用于方差估计**，改用保守规则：
  ① 同研究同结局的表格 SD；② 同 Domain 同结局其他研究的 SD 中位数；
  ③ 仍无 → 该条只进域级合并并在输出表标注 `sd_imputed: domain_median`。
- 缺 SD 且无任何来源 → 排除该条并计入 PRISMA。

### 2.4 方向统一
指标按临床含义统一为「**正值 = 褪黑素优于安慰剂**」：
- 越大越好：VO₂max、跳跃高度/距离、1RM、力竭时间、YYIRT 距离、SOD、GPx、TAC、FRAP、GSH、BAP、ORAC、睡眠效率、总睡眠时间。
- 越小越好（取负）：冲刺/敏捷/5-STST/5-JT 用时、CK、LDH、MDA、AOPP、LPO、NOx、CRP、IL-6、TNF-α、WASO、入睡潜伏期、Hooper 睡眠质量分（AU）。
- 每条的 `direction` 由 `extraction/harmonized/outcome_direction.yaml` 显式登记，未登记即报错（不允许默认）。

## 3. 对比层（contrast layer）

- 主分析 = **每研究每域一条对比**（预先指定，规则见下），做域级合并 → 保证研究间独立。
- 同一研究同域内的其余对比不丢弃，进入**三水平模型**（域 → 研究 → 对比）与 RVE 稳健性分析。
- 选取顺序（写成代码，不可逐案辩解）：
  1. 安慰剂对照的完整配对（同一时点）；
  2. 若只有不同时点，取**主时点**（§4）；
  3. 仍未定 → 取该域内**结局家族的代表性指标**（睡眠：睡眠效率 > 总睡眠时间 > 潜伏期 > WASO；表现：跳跃/冲刺 > 力量 > 力竭时间；氧化：MDA > AOPP > SOD > TAC；炎症：CRP > IL-6 > TNF-α > CK > LDH）；
  4. 结局家族并列 → 剂量最高的一条。
- **多臂研究**（4 臂 5 项、3 臂 4 项、6 臂 1 项）：
  主分析合并全部褪黑素臂与共享对照算一条对比（对照不重复计数）；
  敏感性：① 只取最高剂量臂；② RVE（`rma.mv` + `robust(cluster=study, CR2)`）。

## 4. 主时点规则
- 急性研究：运动后**最近的一次测量**（≤60 min；若只有多时点，取运动后即刻与 60 min 各作一条进敏感性）。
- 长期研究（≥1 周）：**最后一次测量的干预后值**（post-intervention）。
- 睡眠研究：**主测量夜**（干预后第一个/最后一个完整睡眠纪录，按原文声明；无声明取最后一夜）。
- 时点自由文本先归一化为 `baseline / post / delta / acute-{min}`，归一化表随产物落盘。

## 5. 合并模型
- 主分析：**随机效应 REML**，`test = "knha"`（Hartung–Knapp 小样本校正），**报 95% 预测区间**。
- 每个域报：合并 SMD、95% CI、95% PI、τ²、I²、Q、k（研究数）、对比数。
- 三水平模型（域 → 研究 → 对比）与 RVE 作为稳健性分析（本综述每域 k = 8–19，CR2 小样本校正不稳，故不作主分析）。
- k ≥ 3 的结局才出单结局森林图；k < 3 只进域级合并。
- **漏斗图 / Egger 检验仅当 k ≥ 10**（本综述仅域级合并可能达线）。

## 6. 偏倚与证据确定性（合并前完成）
- **RoB 2**：平行研究用 RoB 2，交叉研究用 RoB 2 crossover 版；**人工双评**（小何 + 独立子 agent 各评一遍，分歧由第三人裁定并记录）。
- **GRADE**：4 个域分别评级（起点随机对照 = 高，按 RoB 2、不一致性、间接性、不精确性、发表偏倚降级）。
- 评级表与理由逐条落盘（`analysis/rob/`、`analysis/grade/`），未完成不得发布合并结果。

## 7. 异质性、亚组、敏感性（预先指定）
- 异质性：I²、τ²、Q、预测区间；I² ≥ 75% 时不下「一致」结论。
- ★ 亚组（冻结后修订，2026-10-19；只作探索，不作结论）：
  1. **人群（主口径）**：共病 / 无共病（二分局，写在纳入标准里的诊断）。
     训练水平（quantified / unquantified）改为**次要**表。
  2. main vs sens；交叉 vs 平行；急性 vs 长期（≥1 周）。
  3. **剂量不再分档**，改连续 `dose_mg` meta-regression（mg 与 log-mg 两个尺度）。
     理由：唯一有药理依据的分界是 0.5 mg（口服 ≤0.5 mg 时血浆褪黑素仍在内源夜间范围内，
     Zhdanova 2001 JCEM 86:4727），而本数据最低剂量 2 mg → 全部在超生理一侧，二分退化；
     原写的 ≤3 / 5–6 / ≥10 是**商业规格**（OTC 常见 1/3/5/10 mg），不是药效学断点。
     档位表降为附录描述统计，并标注「商业规格，非药效学依据」。
  4. 亚组与元回归一律 **k ≥ 10 才作结论**（Cochrane 常规），低于此标 exploratory；
     某亚组 < 2 项时组间 QM 不可算，直接写明 skipped。
  5. 组间检验用 `rma(mods=~factor)` 的 `QM`：metafor 在 `test="knha"` 下报的是 **F 统计量**，
     df = (m−1, k−m)；剂量回归另看斜率、CI、R² 与**逐条剔除的杠杆点诊断**（见 §10.2）。
- 敏感性（全部预先指定，逐项报告结果变化）：
  1. r = 0.2 / 0.5 / 0.8；
  2. 排除 40 行中位数换算条目；
  3. 排除图上取点条目；
  4. 排除 `R0170`（本就无数据，仅记录）；
  5. 多臂：合并臂 vs 最高剂量臂 vs RVE；
  6. leave-one-study-out 与 leave-one-cohort-out；
  7. 按课题组剔除（Sfax / Granada / 突尼斯三组各剔除一轮）；
  8. 主时点替换（急性研究取即刻 vs 60 min）；
  9. 仅 RoB 2 低风险研究；
  10. 固定效应模型（仅作对照，不作结论）。

## 8. 可复现性
- 全链条脚本：`extraction/`（YAML → `records.json` + `effects.csv`）→ `extraction/harmonized/`（单位与方向归一）→ `analysis/contrasts.py`（对比层 + 效应量）→ `analysis/R/metafor.R`（合并）→ `output/`。
- 每个数字必须能从 `effects.csv` + 脚本重算；产物带生成时间、输入文件哈希、脚本版本。
- R 侧记录 `sessionInfo()` 与 `metafor` 版本；Python 侧记录 `pandas` / `numpy` 版本。**不用未锁定版本的在线服务**。

## 9. 报告口径
- 主文：4 个域的合并 SMD + 森林图 + I² + 预测区间 + GRADE 表 + PRISMA 流程图。
- 附录：单结局森林图（k ≥ 3，共 15 个）、RoB 2 逐研究表、全部敏感性分析表、逐条效应量原始表（含 `source_kind`、`source_ref`、`r_source`、`sd_imputed`、`sigma_approx`）。

## 10. 偏差记录（冻结后新增）

| 日期 | 偏差 | 理由 | 影响 |
|---|---|---|---|
| 2026-10-18 | 纳入后排除 2 项研究（`R0323` 无随机化依据、`R0072` 四类结局为零） | 全文核对发现 | 报告数 41→39；PRISMA 已同步 |
| 2026-10-18 | 中位数条目用 `σ ≈ IQR宽度/1.349`，不进单结局合并 | 原文只给 IQR 宽度，Wan 法不可用 | 见 §2.3；敏感性第 2 项 |
| 2026-10-18 | `R0170` 纳入但无数据（付费墙 + 公开版本只有 2 页） | 取全文失败 | 该研究不进合并，PRISMA 标注 |
| 2026-10-18 | 图上取点改用 `paiksca/digitize`（MIT），自写工具作废 | 手工判据在读端帽/标定上出过系统性错误 | 读数已用原文自述百分比二次验证 |
| 2026-10-19 | Δ 时点维持「取结局方向的反号」（`flip: true`），不改「Δ 恒为 higher」 | 见下条理由；曾试点改为恒 higher，被 `19390211` 原文推翻 | 24 条 Δ 对比符号与原文一致 |
| 2026-10-19 | `GRANADA-100MG-4W` 的 24 条睡眠行由 SD 改为 SE | 原文 `R0289` 写明汇总值用 SE；`R0273` 的 12 行确为 SD | 该研究睡眠域 yi 变小（原被高估） |
| 2026-10-19 | `R0375` 的 SJ/CMJ、`R0322` 的 MDA/TAS 缺离散度：前者借同域 SD，后者只能剔除 | 图题注未声明误差类型；TAS 误差棒与柱顶粘连读不出 | 敏感性分析第 11 项（剔除借用 SD 条目） |
| 2026-10-19 | `19390211` 同时有 Δ 与派生 post（`pre − Δ`）两套值时，主分析取 `post`，Δ 只做敏感性 | 与其它研究报告 post 的口径一致 | 该研究进域级合并 1 条 |
| 2026-10-19 | 补入 `R0273` 图上取点的 13 个 redox 结局（其中 7 个新 canonical outcome） | 这些结局只在图里有数值，Table 1 未给 | 氧化域多 10 条主对比 |
| 2026-10-19 | 缺 SD 的借用改为**按变异系数折算**，不是借绝对 SD 中位数 | 借绝对 SD 跨数量级出错（`GRANADA-100MG-4W` 的 aopp 借到 0.05，算出 yi=+129.4） | 借用条目 yi 回到合理量级；敏感性第 11 项 |
| 2026-10-19 | 合并层改由对比层算效应量，R 只做合并（`metafor.R` 重写） | 旧版把每行当双臂平行，交叉设计（20/32 项）方差会算大 | 合并值变化；R 与 Python 逐格比对 0 差 |
| 2026-10-19 | 合并按 `pool_key = family|construct|unit|time_kind` 分组 | 原把急性与长期、Δ 与绝对值混进同一池（实测 9 个池混了 time_kind） | 合并单元 34 个，可合并 11 个 |
| 2026-10-19 | `R0322` 的 `tas` 从与 `tac` 共用构念改为独立构念 | 两者是不同测定，共构念会让缺 SD 的借用跨测定串用 | TAS 仍 k=1，不进合并 |
| 2026-10-19 | `R0170` 的全文字段由 `include` 改判 `not_retrieved`（E12） | 取全文穷尽后确认不可获取（bronze OA 但出版商侧 Restricted access；`downloadpdf` 重定向回 HTML 文章页；解析只有 2 页预览） | 报告数 39→38，纳入研究数不变；PRISMA「未获取 1」 |
| 2026-10-19 | `R0378` 与 `R0389` 合并为一项研究 `SOUSSI-DAYTIME-8` | 同为 8 名体育教育男生 / 6 mg / 09:00 / 跑台 45 min @60% MAS；R0378 只报 CRP、R0389 只报 SOD，两池不重叠 | 研究数 32→**31**；RoB 2 表少一行重复评定；**任何已发布的效应量不变** |
| 2026-10-19 | 剂量亚组由三档改为**连续 meta-regression** | 唯一药理分界 0.5 mg 在本数据（最低 2 mg）内不可用；原档位是商业规格 | §7 条目 3；新增 `moderators.csv` |
| 2026-10-19 | 人群亚组改二分「共病 / 无共病」，训练水平降为次要 | 共病写在纳入标准里、可核验；训练水平是连续量且无统一切点（ACSM 以 VO2max 或训练量定义，本资料 3 项两项都没给） | 新增 `subgroups.yaml`（31 条逐项写明依据）与 `subgroups.csv` |
| 2026-10-19 | 亚组与剂量回归一律 k ≥ 10 才作结论；元回归另报「逐条剔除的杠杆点诊断」 | 本综述 inflammation 的「显著剂量-反应」完全由 100 mg 那一项驱动（剔除后 p 0.002→0.166），只报总模型 p 会给假结论 | `moderators.csv` 的 `influential` 列；见 §10.3 |
| 2026-10-19 | 域级主估计把协议的两轨（主分析=无共病 / 敏感性=有共病）混在同一个合并里，人群只在亚组层分开 | 域级 `k_studies` 恰为两轨之和（inflammation 3+7=10、performance 2+17=19）；协议的双轨是对**分析**的分轨，不只是纳入范围 | 域级 g 是两轨的混合估计；GRADE 的 `indirectness` 据此判 serious（见 §10.4） |
| 2026-10-19 | `GRANADA-100MG-4W` 睡眠表（`Table 4`）的 8 条效应量**保留 SE 口径**，但把「原文自相矛盾」写进例外白名单，并新增 `no-granada` 敏感性组 | `R0289` Methods 写 `mean ± standard error`、TABLE 4 题注写 `Data are the means ± SD`——同一篇论文两种声明。量级判定：按 SD 读该研究 g=14.2（不可能），按 SE 读 g=3.97；睡眠效率的个体间 SD 不可能是 0.1–0.3 个百分点 | `extraction/verify-exceptions.yaml` 2 条（共 8 行）；`assemble --verify` 由「不符 8 条」回到「不符 0 条，豁免 8 条」；`no-granada` 组睡眠域 k=6、g=0.929 [−0.198, 2.057]（见 §10.5） |

### 10.1 ★ Δ 极性的判据（不要去“修”成恒 higher）

同一篇原文（`19390211`）把两件事都写明了：

1. 方法：`Δ = values_before − values_after`；
2. 结果：`Only in the non-dominant leg, the MG presented lower Δ (PCF) … (i.e., higher
   increase in these parameters) in comparison with PG`（原文 §3）。

→ 当结局是「越大越好」的力量（PCF/PCE）时，**Δ 越低说明力量增幅越大（越好）**；
当结局是「越小越好」的用时（NHPT/5-STST）时，**Δ 越高才是改善**。
两种极性都能用一个「取反号」统一，所以 `analysis/timepoint_map.yaml` 的 Δ 时点
一律 `flip: true`（对比 = sign·(mel − pla)，符号取反后正值仍 = 褪黑素更好）。

**自检口径**：`pcf-90` 主腿 Δ（mel `+3.387` vs pla `+6.130`，已反号）→ 效果量为**负**
（安慰剂力量增幅更大）；同研究非主腿 → 为正（原文只在这一侧报 MG 更优）。

### 10.2 合并层的实现口径（冻结后补记，2026-10-19）

效应量在**对比层**算好（`hedges_g_parallel` / `hedges_g_crossover`），
`analysis/R/metafor.R` 只做合并 —— 因为 `escalc(measure="SMD")` 只有一个方差公式，
它默认双臂平行；把 20 项交叉设计按平行算会系统性高估方差。

- 模型：`rma(yi, vi, method="REML", test="knha")`；区间与预测区间用 `t(k−1)`。
- 域级（`family`）为**主口径**，构念级（`pool_key`）为次要；两者都出森林图。
- 漏斗图与 Egger 检验**仅当 k ≥ 10**（SAP §5）；`leave1out` 仅当 k ≥ 3。
- Δ 时点默认**排除**（只做敏感性），`--include-delta` 纳入并明确标注。
- 借用 SD 的条目默认纳入并标注，`--exclude-imputed` 剔除。
- 独立复核：`analysis/python/statsmodels_check.py` 用 numpy/scipy 重算一遍并与 R 的
  `domains.csv` 逐格比对；效应量与区间容差 1e-3，`I²`/`Q`/`p_Q` 容差 2e-2
  （百分数量纲 + τ² 贴在 0 上时的优化器差异）。不一致即非零退出 —— 全流程 5 组敏感性
  实测最大绝对差均为 0。
- 敏感性分析由 `python -m workflows.review.analysis.sensitivity` 一次跑完五组。

### 10.3 亚组与剂量回归的实现口径（冻结后补记，2026-10-19）

归属表是**人工裁定**，每条判断都写明原文依据（`analysis/subgroups.yaml`）：
`population`（clinical/non-clinical）、`training`（quantified/unquantified/clinical）、
`dose_mg`。多条件臂（`R0042` 的 5/12.5/20 mg、`R0375` 的 5 与 8 mg）在对比层已被合并成
一个臂，剂量取条件均值，已在 `dose_mg_note` 记明。不在表里的研究留空并报提醒，**不做推测**。

`metafor.R --subgroups` / `--moderator dose` 与 `statsmodels_check.py --subgroups` /
`--moderator dose` 两条独立路径必须逐格一致（含 `QM`/`qm_df1`/`qm_df2`/`R²`/斜率）。
两处实现细节容易做错，故记在此：

1. `rma(mods = ~ x)` 的公式在**调用环境**里求值 → 必须显式传 `data=`，否则报
   `object 'x' not found`，而它会被 tryCatch 写成注释后静默留下空的 `QM`。
2. `test="knha"` 时 metafor 的 `QM` 是 **F 统计量**（Wald 二次型 ÷ 分子 df），
   `QMdf` 是**长度 2 的向量**（分子、分母）；当标量写进 `data.frame` 会把每行复制成两行。
3. 单协变量（df=1）时二次型与 F 相等，所以只有三水平以上的因子才看得出区别。
4. 杠杆点诊断把两种情形都点名：**剔除后 p 跨过 0.05**，以及**剔除后调节变量再无变异**
   （后者说明该点单独撑起了整个剂量梯度）。

**主分析结果（现行）**：

| 域 | k | g [95% CI] | I² | 剂量斜率（mg） | 人群 QM |
|---|---|---|---|---|---|
| performance | 19 | +0.167 [+0.023, +0.310] | 3.9% | −0.019（p=0.53） | 1.83（1, 17）p=0.19 |
| sleep | 7 | +1.403 [−0.006, +2.812] | 92.8% | +0.034（p=0.053）[探索] | 不可算（clinical k=1） |
| oxidative | 10 | +1.331 [−0.093, +2.754] | 93.9% | +0.005（p=0.83） | 不可算（clinical k=1） |
| inflammation | 10 | +0.279 [−0.629, +1.188] | 92.1% | +0.043（p=0.002）[★ 杠杆点] | 0.47（1, 8）p=0.51 |

★ inflammation 的剂量斜率虽 p=0.002，但剔除 `GRANADA-100MG-4W`（100 mg，比第二高剂量
高 5 倍）后 p=0.166 → **不得作为结论报出**。sleep 的剂量斜率同属探索，且被 `R0253` 翻转。

### 10.4 GRADE 评分的实现口径（冻结后补记，2026-10-19）

- 起点 `high`（全部为 RCT）；`serious` 降 1 级、`very_serious` 降 2 级；**下限 `very_low`（最多降 3 级）**。
  初版契约写「净降级不超过 2 级」而括号里写「最低到 `very_low`」——**自相矛盾**，两位评分人据
  此得出 8 处 `certainty` 分歧，已改。
- `inconsistency` 只看 I² 与研究间方向（I² ≥ 75% 或亚组反号 → `very_serious`）。
  **预测区间跨 0 归 `imprecision`**，不归 `inconsistency` —— 区间过宽是不精确，不是异质性。
  初版契约把 PI 跨 0 当 `inconsistency` 判据，导致 `performance` 被误判 `very_serious`。
- `publication_bias` 以合并层 Egger 检验为准（k ≥ 10，p < 0.10 判 `serious`）。
  ★ Egger 只存在 `results.json` 的 `domains` / `constructs_k2` 键里，`domains.csv` / `constructs.csv`
  **不导出**这两列；底稿生成器起初漏读 → 底稿无发表偏倚证据 → 两位评分人只能写「未评估」并误判
  `serious`。`grade.py` 已加 `load_meta_json` 补出底稿 §2.1。
- `indirectness` 以协议 `criteria.txt` 的 P / I / O 清单为准（契约 §2.4）。三条实据：
  ① 域级池把协议划给敏感性轨的共病人群混进主轨（域级 `k_studies` 恰为两轨之和）；
  ② 池内含协议 O 清单之外的标志物（`inflammation` 的 `ck`——肌损伤标志物；`oxidative` 的 `aopp`、`uric-acid`）；
  ③ 剂量含远超其余研究的超常值（100 mg，第二高 20 mg）。
  ★ 健康 / 训练人群**就是**协议的目标人群、单次急性给药**在**干预范围内 → 二者都不构成间接性。
- 双评：两轮独立评分。第一轮 36 条判定 88/36 里 8 处分歧（降级领域加权 kappa 0.595、
  最终信度 kappa 0.000）；修契约与底稿后第二轮 **36 条全一致（两个 kappa 均 1.000）**，无需改判。
- `--compare` 的加权 kappa 分别按降级领域的 3 档与最终信度的 4 档计算（`_linear_kappa(levels=)`）。

**最终信度**：

| 域 | risk_of_bias | inconsistency | indirectness | imprecision | publication_bias | 净降级 | 信度 |
|---|---|---|---|---|---|---|---|
| performance | not_serious | not_serious | not_serious | serious | serious | −2 | **low** |
| sleep | serious | very_serious | serious | serious | not_serious | −5 | **very_low** |
| oxidative | not_serious | very_serious | serious | serious | serious | −5 | **very_low** |
| inflammation | not_serious | very_serious | serious | serious | not_serious | −4 | **very_low** |

结论：**证据质量不足以支持褪黑素改善任一家族结局**。`performance` 是唯一效应稳健的域
（g 0.154–0.200，五组敏感性 CI 全不含 0），但仍因 Egger p=0.017（小样本效应）与
预测区间跨 0 降到 `low`。

### 10.5 ★ `GRANADA-100MG-4W` 离散度的原文矛盾与处置

`R0289` 同一篇论文给出两种互相排斥的声明：

- `fulltext/parsed/R0289/full.md:114`（Methods）：`Group data were expressed as mean ± standard error.`
- `fulltext/parsed/R0289/full.md:184`（TABLE 4 题注）：`Data are the means ± SD.`

**本综述采用 Methods 的 SE 口径**，判据是量级而非文字：

- 按 SD 读，该研究睡眠效率的 Hedges' g = **14.2**（效应量 14 在运动科学里不存在）；按 SE 读
  g = **3.97**。
- 睡眠效率的个体间 SD 不可能是 0.1–0.3 个百分点（原文格为 `92.8 ± 0.1` 量级）。
- 夜间觉醒次数 `2.60 ± 0.079`：按 SD 读 SD=0.079 次，按 SE 读 SD≈0.27 次；后者才符合
  「固定作息、同质队列、多夜均值」。

**处置三层，缺一不可**：

1. **写进例外白名单**。`extraction/verify-exceptions.yaml` 显式登记 2 条通配规则
   （`GRANADA-100MG-4W-sleep-efficiency-*`、`-awakenings-*`，共 8 行），豁免项仅
   `dispersion-kind` 一条，`reason` 必填且须引原文原句。缺 `reason` 时 `verify.py`
   直接 `ValueError`——**例外是受审计的，不是静默跳过**。豁免条数由 `assemble --verify`
   打印出来，不进问题清单（否则调用方永远返回码 1）。
2. **加敏感性组**。`sensitivity.py` 的 `RUNS` 新增 `no-granada`，经 `metafor.R` 与
   `statsmodels_check.py` 各自新支持的 `--exclude-study ID`（可重复）剔除整项研究；
   该组 R↔Python 逐格差仍为 0。
3. **正文并排报**。主分析与 `no-granada` 的睡眠域数值必须同时出现，不得只报前者。

**`no-granada` 结果（r=0.5，剔除整项研究）**：

| 域 | 主分析 k 与 g [95% CI] | `no-granada` k 与 g [95% CI] |
|---|---|---|
| performance | 19，0.167 [0.023, 0.310] | 19，**不变** |
| sleep | 7，1.403 [−0.006, 2.812] | 6，**0.929 [−0.198, 2.057]** |
| oxidative | 10，1.331 [−0.093, 2.754] | 9，1.368 [−0.292, 3.029] |
| inflammation | 10，0.279 [−0.629, 1.188] | 9，0.010 [−0.407, 0.426] |

★ 读法：`no-granada` 是**整项研究剔除**，不是只剔那 8 行睡眠数据 —— 它同时去掉了该研究的
1 条 inflammation 与 1 条 oxidative 条目，所以 inflammation 由 0.279 掉到 0.010 与离散度
之争**无关**，属剔除整项的副作用，不得当成「离散度问题影响了炎症域」的证据。
对睡眠域而言该组恰好等价于只剔那 8 行，**这才是本节的答案**：睡眠域本就处于显著边缘
（主分析 p=0.0508），换成更保守的估计后 p=0.088，**方向与不显著性都不变**，
GRADE 对睡眠域的 `very_low` 不因此改动。

★ 同时说明为什么有些数字对不上：`10.1016/j.clineuro.2024.108165` 在 `analysis/input/sleep.csv`
里却不在睡眠域池中——它 `time_kind = delta`，`metafor.R` 按 §3 排除变化量，**不是遗漏**。
