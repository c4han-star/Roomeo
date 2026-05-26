# MyRoomeo 测验记分与角色匹配逻辑

> **实现位置：** [`quiz.html`](../quiz.html) 内联 JavaScript  
> **产品规格参考：** [`docs/result page.md`](./result%20page.md) 第 4–7 节（设计层说明，与代码略有差异）

---

## 结论：现在有没有这套逻辑？

**有，但分三层，成熟度不同：**

| 层级 | 是否已实现 | 作用 |
|------|------------|------|
| **1. 角色类型判定** | ✅ 已实现 | 12 道题答完后，算出 6 种动物中的 1 种 |
| **2. 四维生活方式辅助分** | ✅ 已实现 | 生成 profile 文案、部分「Why you」bullet，**不决定**最终动物 |
| **3. 两人 compatibility 分数** | ❌ 未实现 | 结果页「Compatibility radar」是**写死的文案**，不是两人答题后的动态计算 |

Compare with a Friend 目前也只是复制邀请链接 + 分享卡片，**不会在朋友答完后自动算出 compatibility score**。

---

## 1. 角色类型判定（核心逻辑）

### 1.1 入口

用户答完 12 题后：

```text
showResults() → resolveType(answers) → 写入 sessionStorage → 渲染结果页
```

相关函数：

- `resolveType(ans)` — 决定动物类型
- `QUIZ[i].votes` — 每题每个选项对应的动物标签

### 1.2 算法：加权投票（Weighted Vote Tally）

对每一道题 `qi`：

1. 读取用户选项索引 `ch`（0 = A，1 = B，2 = C，3 = D）
2. 取出 `QUIZ[qi].votes[ch]`，这是一个**动物 slug 数组**，例如 `['owl', 'beaver']`
3. 该选项给每个标签加 **`1 ÷ 标签数量`** 分  
   - 单标签选项：+1.0  
   - 双标签选项：各 +0.5  
   - 三标签选项：各 +0.333…

12 题全部累加后，6 个动物各有一个总分：

```text
tally = { beaver, cat, owl, fox, bunny, turtle }
```

**得分最高者即为结果类型。**

### 1.3 平局规则（Tie-break）

若多个动物同分，按固定优先级取第一个：

```text
beaver → owl → turtle → fox → bunny → cat
```

代码中的 `tieOrder` 数组即此顺序。  
这意味着：**同分情况下 Beaver 最优先，Cat 最靠后。**

### 1.4 伪代码

```javascript
function resolveType(ans) {
  tally = { beaver: 0, cat: 0, owl: 0, fox: 0, bunny: 0, turtle: 0 }

  for each question qi:
    tags = QUIZ[qi].votes[ ans[qi] ]
    weight = 1 / tags.length
    for each tag in tags:
      tally[tag] += weight

  return animal with max tally (use tieOrder on tie)
}
```

### 1.5 设计意图

- **多标签选项**表示「这个答案同时像两种动物」，所以分数分摊，避免某一题权重过大。
- 动物类型由**全卷投票总和**决定，而不是「某一维最高」。
- 与 [`result page.md`](./result%20page.md) 里「4 个维度映射到 6 种动物」的产品描述一致，但**代码实现是离散投票表**，不是连续维度聚类。

---

## 2. 题目与维度结构

共 **12 题**，分 4 组（每组题数不同）：

| 维度 | 题号（0-based） | 题数 | Section |
|------|-----------------|------|---------|
| A. Cleanliness & Initiative | Q0–Q2 | 3 | 清洁度与主动性 |
| B. Social Energy & Guests | Q3–Q5 | 3 | 社交能量与访客 |
| C. Structure vs Flexibility | Q6–Q9 | 4 | 规则 vs 灵活 |
| D. Presence & Engagement | Q10–Q11 | 2 | 在家存在感 |

每题 4 个选项，每个选项在 `votes` 里绑定 1–4 个动物 slug。

### 示例（Q0）

**题目：** 半夜渴了，会不会喝室友的 Sprite？

| 选项 | 标签 | 含义倾向 |
|------|------|----------|
| A | owl, beaver | 边界感强 / 规则意识 |
| B | owl, turtle | 先沟通、偏谨慎 |
| C | fox, bunny | 有共享 vibe 时较随意 |
| D | cat | 先做了再说 |

---

## 3. 四维分数（辅助逻辑，不决定动物）

### 3.1 选项分值

```javascript
answerScores(ans): 每题 score = 4 - optionIndex
// A=4, B=3, C=2, D=1
```

### 3.2 维度汇总

```text
Cleanliness     = Q0 + Q1 + Q2        （3 题，满分 12）
Social energy   = Q3 + Q4 + Q5        （3 题，满分 12）
Structure       = Q6 + Q7 + Q8 + Q9   （4 题，满分 16）
Engagement      = Q10 + Q11           （2 题，满分 8）
```

### 3.3 等级标签 `traitLevel(sum, invert, n)`

按题目数量 `n` 动态算阈值（以 3 题为基准）：

- **High 阈值：** `round(9 × n/3)`
- **Low 阈值：** `round(5 × n/3)`
- 介于两者之间 → **Moderate**

**Social energy 使用 `invert: true`：** 分数越高，社交能量标签反而越低（Quiet），因为 A 选项代表更偏安静/边界。

### 3.4 这些分数用在哪里？

| 函数 | 用途 | 是否影响动物类型 |
|------|------|------------------|
| `deriveLifestyle(ans)` | Profile Step 2 预填 rhythm / clean / social 文案 | ❌ |
| `getWhyBullets(ans, typeKey)` | 结果页「Your answers suggest that you」动态 bullet | ❌ |
| `buildTraitGridHtml(ans)` | 四维网格 HTML（**已写函数，当前 UI 未挂载**） | ❌ |

### 3.5 结果页上的百分比 Stats

结果页 `Cleanliness: 100%` 等数据来自 `TYPES[typeKey].stats`，是**每种动物写死的展示文案**，不是从 `answerScores` 实时算出来的。

---

## 4. 六种动物与 compat 文案

动物元数据都在 `TYPES` 对象里，包括：

- `name`, `emoji`, `subtitle`, `shareTrait`
- `stats`, `roast`, `whatLiving`, `scenarios`
- **`compat`**：每种类型固定 2 条（1 个 Soulmate + 1 个 Roommate war）

例如 Beaver：

```javascript
compat: [
  { name: 'The Owl', line: 'Soulmate — ...' },
  { name: 'The Cat', line: 'Roommate war — ...' }
]
```

**这不是根据两个用户答题动态匹配的**，只是结果页叙事内容。

---

## 5. 尚未实现的「真实匹配」

以下在产品文档里提到过，但**当前代码没有**：

1. **两人 compatibility score**  
   用户 A + 用户 B 各答完题后，计算 0–100 分或等级。

2. **Compare with a Friend 自动对比**  
   朋友通过链接答完后，展示双方类型对照卡（目前只有邀请人的 compare 分享卡）。

3. **Waitlist / 后端匹配**  
   没有 server-side scoring；答案存在 `sessionStorage`（`roomeo_quiz_answers`, `roomeo_type`）。

4. **Stats 百分比与答题联动**  
   UI 上的 100% / 22% 等是静态 copy，不是维度分换算。

---

## 6. 若要做「两人匹配分」，建议方向

在现有 `resolveType` + `answerScores` 基础上，可以这样扩展（**尚未编码**）：

### 方案 A：类型矩阵（简单）

预置 6×6 compat 矩阵（Soulmate / Neutral / War），两人类型查表即可。  
与现有 `TYPES[].compat` 叙事一致，实现成本最低。

### 方案 B：四维距离（更细）

1. 两人各算 4 维向量（Cleanliness, Social, Structure, Engagement）
2. 算加权欧氏距离或余弦相似度
3. 映射到 compatibility 百分比 + 文案 tier

### 方案 C：混合（推荐）

- **Primary type** 仍用现有 `resolveType` 投票
- **Match score** 用四维距离
- **Narrative**（Soulmate / War 一句话）用类型矩阵或规则引擎

---

## 7. 调试与预览

| 方式 | 说明 |
|------|------|
| URL hash | `quiz.html#turtle` 直接打开某类型结果（可无完整答题） |
| Query | `?previewResult=beaver` 预览指定类型结果页 |
| Session | 完整答题后 `roomeo_type` + `roomeo_quiz_answers` 保存在浏览器 |

---

## 8. 关键代码索引

| 符号 | 文件位置（约） | 说明 |
|------|----------------|------|
| `QUIZ` | quiz.html ~2823 | 12 题 + 每选项 `votes` |
| `TYPES` | quiz.html ~2983 | 6 种动物文案与 compat |
| `resolveType()` | quiz.html ~3310 | **类型判定主逻辑** |
| `answerScores()` | quiz.html ~3287 | A=4…D=1 |
| `traitLevel()` | quiz.html ~3292 | High / Moderate / Low |
| `deriveLifestyle()` | quiz.html ~3461 | Profile 文案 |
| `getWhyBullets()` | quiz.html ~3498 | 动态 why bullets |
| `showResults()` | quiz.html ~3883 | 提交后触发计分 |

---

## 9. 一句话总结

**现在的记分逻辑是：12 题加权动物投票 → 得出 1 个类型；四维分数只辅助文案，不决定类型；compat 和 stats 是预设内容，不是两人动态匹配。**  
若产品需要「朋友答完后显示 compatibility score」，需要在上述基础上新增一层匹配算法与 UI。
