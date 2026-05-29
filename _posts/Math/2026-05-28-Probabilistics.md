---
title: "概率论"
date: 2026-05-28 00:00:00 +0800
categories: [数学]
tags: [数学, 概率伦]
author: wjj
toc: true
math: true
---

# 基本公式

$$
\overline{(A \cup B)} = \overline{A} \cap \overline{B}
$$
$$
\overline{AB} = \overline{A} \cup \overline{B}
$$

---

$$
P(A) = 1 - P(\overline{A})
$$

---

$$
P(A \cup B) = 1 - P(\overline{A \cup B}) = 1 - P(\overline{A} \cdot \overline{B})
$$
$$
P(AB) = 1 - P(\overline{AB}) = 1 - P(\overline{A} \cup \overline{B})
$$

---

$$
A \cup B = A \cup \overline{A}B = B \cup A\overline{B} = A\overline{B} \cup AB \cup \overline{A}B
$$
$$
P(A \cup B) = P(A \cup \overline{A}B) = P(B \cup A\overline{B}) = P(A\overline{B} \cup AB \cup \overline{A}B) = P(A\overline{B} + AB + \overline{A}B)
$$

---

若 $B_1, B_2, B_3$ 为完备事件组，则：
$$
A = AB_1 \cup AB_2 \cup AB_3
$$
$$
P(A) = P(AB_1) + P(AB_2) + P(AB_3)
$$

---

$$
P(A + B) = P(A) + P(B) - P(AB)
$$
$$
P(A + B + C) = P(A) + P(B) + P(C) - P(AB) - P(BC) - P(AC) + P(ABC)
$$

---

若 $A_1, A_2, \cdots, A_n$（$n \geq 2$）两两互斥，则：
$$
P\left(\bigcup_{i=1}^{n} A_i\right) = \sum_{i=1}^{n} P(A_i)
$$

---

$$
P(A|B) = \frac{P(AB)}{P(B)} \quad (P(B) > 0)
$$

---

$$
\begin{aligned}
P(AB) &= P(B)P(A|B) \quad (P(B) > 0) \\
&= P(A)P(B|A) \quad (P(A) > 0) \\
&= P(A) + P(B) - P(A + B) \\
&= P(A) - P(A\overline{B})
\end{aligned}
$$
---

**全概率公式** 
若 $A_1, A_2, \cdots, A_n$（$n \geq 2$）为完备事件组， $P(A_i)>0(i=1,2,\cdots, A_n)$ ，则

$$
P(B) = \sum_{i=1}^{n} P(A_i)P(B|A_i)
$$

---
**贝叶斯公式**

$$
P(A_j|B) = \frac{P(A_jB)}{P(B)} = \frac{P(A_j)P(B|A_j)}{\sum_{i=1}^{n}P(A_i)P(B|A_i)} \quad (j = 1,2, \cdots ,n)
$$
