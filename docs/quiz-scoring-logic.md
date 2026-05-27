# MyRoomeo 测验记分与角色匹配逻辑

> **实现位置：** [`quiz.html`](../quiz.html) 内联 JavaScript（`QUIZ`、`TYPES`、`resolveType`）  
> **产品规格参考：** [`docs/result page.md`](./result%20page.md)  
> **English version:** [`quiz-scoring-logic-en.md`](./quiz-scoring-logic-en.md)

---

## 0. 快速结论

| 问题 | 答案 |
|------|------|
| 有没有记分逻辑？ | **有**，在 `quiz.html` 前端跑 |
| 怎么决定你是哪种动物？ | 12 题每题选一个选项 → 给 6 个动物**加权投票** → 总分最高者胜出 |
| 「多少分是什么角色」？ | **不是**「满 100 分 = Beaver」这种固定分数线；是 **6 个动物各自累积分，谁最高是谁** |
| 结果页百分比 Stats | **写死文案**，不是从答题实时算的 |
| 两人 compatibility | **未实现**动态算分；compat 是预设叙事 |

---

## 1. 六种角色一览

代码里用 **slug** 作 key，页面上用 **The X** 显示名：

| slug | 显示名 | Emoji | 在产品维度上的典型画像 |
|------|--------|-------|------------------------|
| `beaver` | The Beaver | 🦫 | 高清洁、高规则、中高在家参与度 |
| `owl` | The Owl | 🦉 | 低社交、高结构、边界感强 |
| `turtle` | The Turtle | 🐢 | 偏宅、中等规则、清洁尚可 |
| `fox` | The Fox | 🦊 | 灵活、偏社交、清洁/规则较松 |
| `bunny` | The Bunny | 🐰 | 高社交、灵活、爱热闹 |
| `cat` | The Cat | 🐱 | 低参与、低清洁、各顾各的 |

每种动物的完整文案（roast、stats、compat 等）在 `TYPES[slug]` 对象里。

---

## 2. 核心算法：加权投票（决定「你是哪种动物」）

### 2.1 流程

```text
用户答完 12 题
  → answers = [0..3, 0..3, ...]   // 每题选项索引
  → resolveType(answers)
  → tally = { beaver, owl, turtle, fox, bunny, cat }
  → 取 tally 最高者
  → 同分则按 tieOrder 优先级
  → 结果写入 sessionStorage.roomeo_type
```

### 2.2 单题怎么加分

对第 `qi` 题，用户选了选项 `ch`（0=A, 1=B, 2=C, 3=D）：

1. 查 `QUIZ[qi].votes[ch]` → 得到动物数组，如 `['owl', 'beaver']`
2. 权重 `w = 1 / 数组长度`
3. 数组里**每个**动物 `+= w`

| 选项绑了几个动物 | 每个动物本题得分 |
|------------------|------------------|
| 1 个 | **+1.0** |
| 2 个 | **+0.5** 各 |
| 3 个 | **+0.333…** 各 |
| 4 个 | **+0.25** 各 |

> 全卷 12 题，**理论单动物上限是 12.0**（12 题都选只含自己的单标签选项）。  
> 实际题库设计下，各动物「每题最优选择」累加后的**实际上限**见下表（因为多数题是双标签分摊）：

| 动物 | 12 题全选「对该动物最有利」选项时的 tally 上限 |
|------|-----------------------------------------------|
| turtle | **8.5** |
| beaver | **8.0** |
| cat | **8.0** |
| owl | **7.5** |
| fox | **7.0** |
| bunny | **6.0** |

### 2.3 怎么读 tally 分数

- tally 是 **0 ~ 约 8.5** 的连续小数，不是百分制
- **没有**「≥7 分就是 Owl」的阈值表
- 只看 **6 个数里谁最大**，例如：

```text
beaver: 5.5
owl:    4.0
turtle: 3.5
fox:    2.0
bunny:  1.5
cat:    1.0
→ 结果：The Beaver
```

### 2.4 平局规则（Tie-break）

若最高分并列，按固定优先级取第一个（**排越前越优先**）：

```text
beaver → owl → turtle → fox → bunny → cat
```

例：`beaver: 6.0` 与 `owl: 6.0` 并列 → 结果仍是 **Beaver**。

### 2.5 伪代码

```javascript
function resolveType(ans) {
  const tally = { beaver: 0, cat: 0, owl: 0, fox: 0, bunny: 0, turtle: 0 };
  for (let qi = 0; qi < 12; qi++) {
    const tags = QUIZ[qi].votes[ans[qi]];
    const w = 1 / tags.length;
    for (const tag of tags) tally[tag] += w;
  }
  const tieOrder = ['beaver', 'owl', 'turtle', 'fox', 'bunny', 'cat'];
  return tieOrder.reduce((best, k) => tally[k] > tally[best] ? k : best, 'owl');
}
```

---

## 3. 完整 Mapping 表：12 题 × 4 选项 → 角色 + 得分

选项索引：**A=0, B=1, C=2, D=3**  
「本题得分」= 选该选项时，**每个**列出的动物获得的分数。

---

### Q1 · A. Cleanliness & Initiative

**题干：** 半夜渴了，室友 asleep，只有室友的 Sprite。

| 选项 | 选此项时加分的动物 | 每个动物得分 |
|------|-------------------|-------------|
| **A** | owl, beaver | 各 +0.5 |
| **B** | owl, turtle | 各 +0.5 |
| **C** | fox, bunny | 各 +0.5 |
| **D** | cat | +1.0 |

---

### Q2 · A. Cleanliness & Initiative

**题干：** 做完饭很累，碗在池子里。

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | beaver | +1.0 |
| **B** | owl, fox | 各 +0.5 |
| **C** | turtle | +1.0 |
| **D** | cat | +1.0 |

---

### Q3 · A. Cleanliness & Initiative

**题干：** 垃圾满溢，没人倒。

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | beaver | +1.0 |
| **B** | owl, bunny | 各 +0.5 |
| **C** | fox, turtle | 各 +0.5 |
| **D** | cat | +1.0 |

---

### Q4 · B. Social Energy & Guests

**题干：** 带人回家，室友提前回来撞见 intimate moment。

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | owl | +1.0 |
| **B** | beaver, turtle | 各 +0.5 |
| **C** | fox | +1.0 |
| **D** | bunny, cat | 各 +0.5 |

---

### Q5 · B. Social Energy & Guests

**题干：** 周五晚上，你和室友都在，理想 vibe？

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | owl | +1.0 |
| **B** | turtle | +1.0 |
| **C** | beaver, fox | 各 +0.5 |
| **D** | bunny | +1.0 |

---

### Q6 · B. Social Energy & Guests

**题干：** 10:30pm 后 FaceTime / 低音量音乐，不算死寂。

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | owl, turtle | 各 +0.5 |
| **B** | beaver, turtle | 各 +0.5 |
| **C** | fox | +1.0 |
| **D** | bunny, cat | 各 +0.5 |

---

### Q7 · C. Structure vs Flexibility

**题干：** 室友霸占浴室，影响你出门。

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | beaver | +1.0 |
| **B** | turtle, owl | 各 +0.5 |
| **C** | fox, cat | 各 +0.5 |
| **D** | owl, beaver | 各 +0.5 |

---

### Q8 · C. Structure vs Flexibility

**题干：** 水槽乱、访客多、quiet hours 没共识，要什么系统？

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | fox, cat | 各 +0.5 |
| **B** | bunny | +1.0 |
| **C** | turtle | +1.0 |
| **D** | owl, beaver | 各 +0.5 |

---

### Q9 · C. Structure vs Flexibility

**题干：** 室友习惯和你不同，你的本能？

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | bunny | +1.0 |
| **B** | owl | +1.0 |
| **C** | turtle, fox | 各 +0.5 |
| **D** | beaver | +1.0 |

---

### Q10 · C. Structure vs Flexibility

**题干：** 室友会怎么形容和你同住？（四选一自述）

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | beaver, owl | 各 +0.5 |
| **B** | turtle | +1.0 |
| **C** | fox, bunny | 各 +0.5 |
| **D** | cat | +1.0 |

---

### Q11 · D. Presence & Engagement

**题干：** 周六你在哪里？

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | turtle | +1.0 |
| **B** | beaver, owl | 各 +0.5 |
| **C** | bunny, fox | 各 +0.5 |
| **D** | cat | +1.0 |

---

### Q12 · D. Presence & Engagement

**题干：** 冰箱室友区漏液，沾到共享区。

| 选项 | 动物 | 得分 |
|------|------|------|
| **A** | beaver, turtle | 各 +0.5 |
| **B** | owl, beaver | 各 +0.5 |
| **C** | fox, turtle | 各 +0.5 |
| **D** | cat | +1.0 |

---

## 4. 各动物在题库里的「出场次数」

下面统计的是：**有多少个选项槽位**里出现了该动物（同一题 A/B 各算一次）。

| 动物 | 在 48 个选项槽位中出现次数 | 说明 |
|------|---------------------------|------|
| beaver | 14 | 清洁/规则题里出现最频 |
| owl | 14 | 边界/安静/结构 |
| turtle | 14 | 居中、温和、偏宅 |
| fox | 12 | 灵活、社交中等 |
| bunny | 9 | 偏社交、少出现在清洁题 |
| cat | 10 | 低参与、D 选项常客 |

**bunny 出现次数最少**，纯靠投票拿第一相对更难；**turtle/beaver/owl** 在 mapping 里覆盖最广。

---

## 5. 计算示例（带完整 tally）

### 示例 A：12 题全选 A

| 动物 | 累积分 | 计算来源 |
|------|--------|----------|
| beaver | **4.5** | Q1×0.5 + Q7×1 + Q8×0.5 + Q10×0.5 + Q11×0.5 + Q12×0.5 |
| owl | 3.5 | Q1×0.5 + Q4×1 + Q5×1 + Q6×0.5 + Q7×0.5 + Q8×0.5 + Q10×0.5 + Q11×0.5 + Q12×0.5 |
| turtle | 2.0 | Q1×0.5 + Q6×0.5 |
| fox | 0.5 | — |
| bunny | 1.0 | — |
| cat | 0.5 | — |

**胜者：The Beaver**（4.5）

### 示例 B：12 题全选 D

| 动物 | 累积分 |
|------|--------|
| cat | **7.0** |
| beaver | 2.0 |
| bunny | 2.0 |
| owl | 1.0 |
| turtle / fox | 0 |

**胜者：The Cat**（7.0）

### 示例 C：「偏 Beaver」路径（非全 A，但每题选对 Beaver 最有利的选项）

选项序列：`A,B,A, B,C,B, A,D,D, A,B,B, B`（字母对应 0–3）

| 动物 | tally |
|------|-------|
| **beaver** | **8.0** |
| owl | 2.5 |
| turtle | 1.0 |
| fox | 0.5 |

**胜者：The Beaver**

### 示例 D：「偏 Turtle」路径

| 动物 | tally |
|------|-------|
| **turtle** | **8.5** |
| fox | 1.5 |
| owl | 1.5 |
| beaver | 0.5 |

**胜者：The Turtle**

---

## 6. 四维分数（辅助用，不决定动物类型）

这是**第二套**分数，和上面的动物 tally **独立**。

### 6.1 选项 → 数值分

```javascript
score = 4 - optionIndex   // A=4, B=3, C=2, D=1
```

### 6.2 四维汇总

| 维度 | 包含题号 | 题数 | 分数范围 |
|------|----------|------|----------|
| Cleanliness | Q1–Q3 | 3 | 3–12 |
| Social energy | Q4–Q6 | 3 | 3–12 |
| Structure | Q7–Q10 | 4 | 4–16 |
| Engagement | Q11–Q12 | 2 | 2–8 |

### 6.3 维度 → 等级（High / Moderate / Low）

阈值随题数缩放（`traitLevel(sum, invert, n)`）：

- High：`sum ≥ round(9 × n/3)`
- Low：`sum ≤ round(5 × n/3)`
- 中间：Moderate

**Social energy 单独 `invert: true`**：同一 sum，A 多 → 标签偏 Quiet（低社交），D 多 → 标签偏 High 社交。

### 6.4 用途（不影响 `resolveType`）

| 函数 | 用途 |
|------|------|
| `deriveLifestyle()` | Profile 第二步预填 rhythm / clean / social |
| `getWhyBullets()` | 结果页动态 bullet（不足 3 条时用 `whyFallback` 补） |
| `buildTraitGridHtml()` | 四维网格（函数已有，**结果页 UI 未挂载**） |

### 6.5 结果页 Stats 百分比

`TYPES[slug].stats` 如 `Cleanliness: 100%` 是**每种动物写死的展示 copy**，不是从第 6 节维度分换算来的。

---

## 7. Compatibility（结果页「Compatibility radar」）

每种动物在 `TYPES[slug].compat` 里**固定 2 条**：

- 1 × Soulmate（合拍）
- 1 × Roommate war（不合）

例 — Beaver：

| 关系 | 对象 | 文案类型 |
|------|------|----------|
| Soulmate | The Owl | 预设一句 |
| Roommate war | The Cat | 预设一句 |

**不是**两个用户答完题后动态计算的 compatibility score。

---

## 8. 尚未实现

1. 两人答完 → 自动算 compatibility %
2. Compare with a Friend 朋友完成后双人对比卡
3. 后端 / waitlist 真实匹配
4. Stats 百分比与答题联动

---

## 9. 调试方式

| 方式 | 用法 |
|------|------|
| Hash | `quiz.html#turtle` 直接看某类型结果页 |
| Query | `?previewResult=beaver` |
| Console | 答完题后 `JSON.parse(sessionStorage.roomeo_quiz_answers)` 看选项数组，对照本文 §3 手算 tally |
| 代码 | 在 `resolveType` 前 `console.log(tally)` 可打印 6 动物分数 |

---

## 10. 代码索引

| 符号 | 约略行号 | 说明 |
|------|----------|------|
| `QUIZ` | quiz.html ~2823 | 12 题 + `votes` mapping |
| `TYPES` | quiz.html ~2983 | 6 角色文案 |
| `resolveType()` | ~3310 | **动物判定** |
| `answerScores()` | ~3287 | 四维用的 A=4…D=1 |
| `traitLevel()` | ~3292 | High/Moderate/Low |
| `showResults()` | ~3883 | 提交入口 |

---

## 11. 一句话总结

**Mapping 规则 = 每题每个选项绑定 1–2 个动物 slug，选中则按 `1/标签数` 加分；12 题加总后最高者即你的角色，同分 Beaver 优先。没有单独的「几分对应什么角色」阈值表——要看 6 个动物的相对高低。**
