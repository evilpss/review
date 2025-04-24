## 文献阅读
**文章信息**
作者：Jie Cao, Amit Goyal, Yajing Wang, Xintong Zhan, and Weiming Zhang*
题目：Opioid Crisis and Firm Downside Tail Risks:  Evidence from the Options Market

---

背景：
The opioid crisis refers to a widespread public health emergency characterized by the  misuse, addiction, and overdose deaths associated with opioid drugs.1 It originated from  the overprescribing and widespread use of opioids in the late 1990s and early 2000s.
Overall, the economic costs associated with  opioid-related overdoses have escalated to a critical level, indicating a crisis situation. The  impact of the opioid crisis extends beyond economic costs and encompasses labor market  disruptions and public finance challenges.
However, little is known about whether and how the potential  adverse impact of the opioid crisis on labor productivity will eventually affect the  probability of extremely negative outcomes, which can severely impact a firm’s financial  health, operations, and overall sustainability.

即：阿片类药物危机，其特征是阿片类药物的滥用、成瘾和过量死亡。自20世纪90年代末和21世纪初以来，阿片类药物的过度处方和广泛使用导致了这一公共卫生紧急情况。阿片类药物危机不仅造成了大量死亡，还带来了显著的经济成本，并对劳动力市场和公共财政构成了挑战。

目的：
explore whether and how firms’ downside tail risks driven by the opioid crisis are priced  in the option market, meaning whether firms exposed to a higher level of opioid crisis risks  exhibit a higher cost of option protection against downside tail risk.

结论：A one-standard-deviation increase in opioid-related death rate leads to an  increase of 0.020 (0.016) in NMFIS (SlopeD), which is approximately 5% of the variables’  standard deviation for both NMFIS and SlopeD.

The empirical finding demonstrates that  the implementation of PDMPs can significantly reduce the opioid-related death rate. Our  staggered Difference-in-Differences (staggered DID) analysis reveals a decrease in 6  downside tail risk for firms located in regions that have implemented PDMPs. This result  lends support to a causal relationship between the opioid crisis and downside tail risk  implied from the option market. Furthermore, we use Propensity score matching (PSM)  and stacked Difference-in-Differences (stacked DID) methods to address potential bias  from the staggered DID method. The results are robust to alternative methods.

In summary, the channel tests show that the effects of the opioid crisis on firm  downside tail risk are driven by its adverse impact on employee productivity, and our  results are more pronounced for firms with higher labor intensity, lower labor supply, and  lower workplace safety.


---

文章创新点：
It is the first to  focus on the relationship between the opioid crisis and investor-perceived downside tail  risk implied from the options market.

It is the first to examine how investors  respond to human capital risks stemming from the opioid crisis and how these risks are  priced in the option market.

The study focuses on the firm uncertainty  related to opioid crisis risk and shows that the risk associated with human capital, one of  the most important assets of the firm, is priced in the option market.

就个人来看，本文的逻辑为：

阿片危机影响劳动者健康 → 减少生产力 → 提高公司业绩的负面极端结果概率 → 被投资者在期权市场中反映 → **体现为更贵的看跌期权保护成本。**
其中，文中用NMFIS和SlopeD来衡量下行尾部风险，即企业资产回报中最负面（左尾）的极端情况发生的可能性。


---

收获：
# 1. 尾部风险的测量因子——NMFIS(负向无模型隐含偏度)，SlopeD(隐含波动率斜率)。
- **NMFIS：量化标的股票收益风险中性分布的不对称性。正值越大，意味着防范下行尾部风险的期权保护成本越高。其计算公式如下：**

$$
\text{NMFIS}_{t,\tau} = -\frac{e^{r\tau}W(t,\tau) - 3\mu(t,\tau)e^{r\tau}V(t,\tau) + 2\mu(t,\tau)^3}{\left[e^{r\tau}V(t,\tau) - \mu(t,\tau)^2\right]^{3/2}}
$$
其中：
$V(t,\tau)$ 是波动率合约的价格。

$W(t,\tau)$ 是立方合约的价格。

$\mu(t,\tau)$ 是风险中性预期下的对数回报。

$r$ 是无风险利率。

- **SlopeD：左尾隐含波动率与期权价格之间的关系，正值越大，表明OTM（深度虚值）看跌期权相对更贵，即防范下行尾部风险的期权保护成本更高。其计算公式为：**
  
$$
\text{SlopeD} = \text{回归系数}
$$

具体来说，SlopeD通过对以下回归得到：

$$
\text{Implied Volatility}_{\text{OTM put}} = \alpha + \text{SlopeD} \times \text{Delta} + \epsilon
$$

其中：
$\text{Implied Volatility}_{\text{OTM put}}$ 是深度虚值看跌期权的隐含波动率。

$\text{Delta}$ 是Black-Scholes Delta，范围从-0.5到-0.1。

$\alpha$ 是常数项。

$\epsilon$ 是误差项。


SlopeD的值越大，表明更深的虚值看跌期权（绝对Delta较小）相对越贵，暗示更高的下行尾部风险保护成本。
The first measure we use is the negative model-free implied  skewness (NMFIS), which quantifies the asymmetry of the risk-neutral distribution of  underlying stock returns. A more positive NMFIS value indicates a shift of the probability  mass under the risk-neutral measure from the right to the left tail, suggesting a higher  cost of option protection against downside tail risk. The second measure is the implied  volatility slope (SlopeD), representing the relationship between left-tail implied volatility  and moneyness. A more positive value of SlopeD indicates that deeper out-of-the-money  (OTM) puts are relatively more expensive, suggesting a relatively higher cost of option  protection against downside tail risk. Therefore, higher NMFIS and SlopeD values  represent higher perceived downside tail risk.

---

# 2. 研究方法学习——DID分析（Difference-in-Differences，双重差分）

- 定义：一种用于评估“政策冲击是否对某些对象产生影响”的常用准实验方法。其核心思想是：**在没有处理（如政策）的情况下，处理组和对照组的趋势应当一致（并行趋势假设）。** 即DID通过比较“政策前后变化差异”，剔除时间趋势和组间差异的共同影响，从而识别政策的“净效应”。
   

- 基本模型表述：

  ```math
  Y_{it} = \alpha + \beta \cdot \text{Post}_{st} + \gamma X_{it-1} + \delta_i + \lambda_t + \varepsilon_{it}
  ```

- \( Y_{it} \)：个体 \( i \) 在时间 \( t \) 的结果变量（如：NMFIS、SlopeD）
  
- \( \text{Post}_{st} \)：处理虚拟变量，如paper中将第 \( s \) 州在 \( t \) 年已经实施PDMP政策则为1，否则为0.
  
- \( X_{it-1} \)：控制变量，包含滞后财务指标（如资产、负债比、利润率等）
  
- \( \delta_i \)：个体固定效应（控制不可观测异质性）
  
- \( \lambda_t \)：时间固定效应（控制宏观趋势）
  
- \( \varepsilon_{it} \)：扰动项

- 核心系数：
  - \( \beta \):解释变量（比如政策变量）对结果变量的边际效应.
  - \( \beta > 0 \):政策提高了结果变量（如风险）
  - \( \beta < 0 \):政策降低了结果变量

其中，分析通过比较**政策实施前后**，**处理组与对照组**之间的变化差异，估计政策的净效应.

>文中采取的Stacked DID方法，核心方法如下
- Stacked DID（堆叠式双重差分）是一种在面对分期政策实施（staggered adoption）时，构造多个局部DID模型，再统一估计的策略。
- 传统DID存在“异步处理偏误（staggered adoption bias）”，当政策在不同时间对不同地区实施时，处理组本身也可能变为对照组，混淆了对照基准。
- Stacked DID分析方法将每个处理时间单独对照“尚未处理”的样本。每一组政策实施构建单独子样本、再合并分析。
- 公式结构如下

  假设我们处理多个时间点 \( g \in G \)，则第 \( g \) 个样本的DID模型为：

  ```math
  Y_{it} = \sum_{k \neq -1} \beta_k^g \cdot \mathbb{1}[\text{EventTime}_{it} = k] + \gamma X_{it} + \delta_i + \lambda_t + \varepsilon_{it}
  ```

  最后将所有 \( \beta_k^g \) 合并为：

  ```math
  \beta_k = \frac{1}{|G|} \sum_{g \in G} \beta_k^g
  ```

---

## DID分析模型延伸

> 多组DID（Multiple Treatment Groups）、动态DID（事件研究法 Event Study）、DID交互项（异质性处理效应，DID with Heterogeneous Effects）
- **多组DID（Multiple Treatment Groups）**
  - 政策分多个等级（如轻度、中度、重度政策），或者多次处理（repeated treatment）时可采用多组DID模型。
  - 其数学表达式可以表述为：

    ```math
    Y_{it} = \alpha + \sum_{k=1}^{K} \beta_k \cdot D_{kit} + \gamma X_{it} + \delta_i + \lambda_t + \varepsilon_{it}
    ```

    - \( D_{kit} \)：第 \( k \) 级别的政策处理虚拟变量
    - \( \beta_k \)：对应不同强度或轮次政策的处理效应
    - 比如将PDMP政策按强度分3组或按时间分3轮推行。

- **动态DID（事件研究法 Event Study）**
  - 该模型用来分析政策在实施前后的**时间路径效应**，以及验证“并行趋势假设”和政策影响的持续性。
  - 其数学表达式可以表述为：
    ```math
    Y_{it} = \alpha + \sum_{k \neq -1} \beta_k \cdot D_{i,t+k} + \gamma X_{it} + \delta_i + \lambda_t + \varepsilon_{it}
    ```

    - \( D_{i,t+k} \)：表示个体 \( i \) 在政策相对第 \( k \) 年的虚拟变量（例如 \( k = -3, ..., +3 \)）。
    - **基准年 \( k = -1 \)** 被排除以避免共线性。
    - 画图：横轴为 \( k \)，纵轴为 \( \hat{\beta}_k \)，灰带为置信区间。

- **DID交互项模型（异质性处理效应）**
  - 研究政策效应**是否因某个特征（如劳动强度高 vs 低）而异**时可采取交互项模型。
  - 其数学表达式表述为：
    ```math
    Y_{it} = \alpha + \beta_1 \cdot Post_t + \beta_2 \cdot Treated_i + \beta_3 \cdot (Post_t \times Treated_i) + \theta \cdot (Post_t \times Treated_i \times Z_i) + \gamma X_{it} + \delta_i + \lambda_t + \varepsilon_{it}
    ```

    - \( Z_i \)：某种异质性维度（如劳动密集行业 = 1）。
    - \( \theta \)：在异质性维度下的**DID交互效应**。
    - 实际应用中常见于 ESG评分、行业类别、劳动力供给等分组检验。


> DID分析方法在实证过程中实证实现方法参考如下

- **固定效应控制**：使用 `entity & year FE` 降低遗漏变量偏误
- **标准误差聚类**：聚类至政策实施单元（如县或州）
- **平行趋势检验**：绘制时间相对事件图验证事前趋势一致性
- **稳健性分析**：
  - 倾向得分匹配（PSM）
  - 替代变量与替代样本测试
  - Placebo test（虚拟处理组）



| 维度       | 建议方法                          |
|------------|----------------------------------|
| 标准误控制 | 聚类到处理单元（如州/县/企业）   |
| 多期处理偏误 | 用 `Stacked DID` 或 `Callaway & Sant'Anna` |
| 并行趋势检验 | 使用 Event Study 图              |

---

# 3.PSM倾向得分匹配法（Propensity Score Matching）

- **PSM 是一种处理选择偏差（selection bias）的准实验方法，适用于非随机实验条件下评估政策效果。**
> 它的核心思想是：找到与“被处理个体”在各方面特征都相似、但未接受处理的对照对象，从而构造“好对照组”。
> 后续时间可以阅读 Guo & Fraser (2015). Propensity Score Analysis: Statistical Methods and Applications.

  - 当处理组与对照组之间存在行业地区等系统性差异的时候，采取PSM方法来消除这部分影响。

- 具体步骤如下：

| 步骤 | 内容 | 说明 |
|------|------|------|
| 1 | 设定处理变量 | 例如文中是否处于阿片高暴露地区或是否受PDMP政策影响 |
| 2️| 构建倾向得分模型 | 用 Logit/Probit 模型预测一个个体被处理的概率 |
| 3️| 进行匹配 | 找到倾向得分接近的处理组与对照组样本（1:1, 1:N） |
| 4️| 匹配后检验协变量平衡性 | 验证处理组和对照组在协变量上是否“相似” |
| 5️| 比较结果变量（或用于DID） | 在匹配样本上进行分析（均值比较或DID） |

- 注意事项与局限

| 局限 | 说明 |
|------|------|
| 匹配质量依赖变量 | 如果漏掉重要协变量，匹配会失真 |
| 可观察性偏差 | 只能控制“可观察”的特征，不能解决隐藏变量偏误 |
| 数据利用率下降 | 匹配过程中会丢弃一部分样本（尤其是非重叠区） |

---

# 个人思考

##  一、变量选取的问题

- 文章使用**县级“药物过量死亡率”作为阿片危机的代理变量**，虽然已有文献支持其合理性，但：
  - 该指标**包含非阿片类药物死亡**（如可卡因、安非他命）。
  - 无法区分死亡因素是“滥用”导致还是“医疗使用”导致。
  - 死亡率指标总是存在一定的滞后性。

- 思考：针对这类型变量选择是否能够从现有的数据结构中选择到一个比死亡率更具代表性的指标呢，比如说通过阿片处方量来估计？或者利用死亡率指标进行数据修正，将非阿片类药物去除并结合医院出具处方数量来修正滥用以及医疗使用影响。


---

## 二、识别策略的外部有效性

- 文章使用了PDMP政策的**渐进实施**做自然实验，但：
  - PDMP只是“限制处方”，**无法全面反映**阿片危机的治理状况。
  - 政策实施的实际效果可能存在**州之间质量差异**。

- 思考：在政策识别上进行修正，比如除了参考PDMP政策外，是否可以考虑非处方类阿片药物治理情况相关的政策？


## 三、区域限制

- 文章内容和数据全部基于美国背景，但
  - **阿片危机是美国特有的健康灾难**。
  - 在欧洲、亚洲等地并不普遍。
  - 无法判断是否为全球现象或局部外部性。

- 思考：
  - 数据扩展是否可以做到更多地区，比如通过**跨国对比研究**来完善研究的合理性。
  - 此外，数据研究是否可类比至其他事件，比如说横向比较 **阿片危机 vs 新冠冲击** 对企业劳动力风险的异同；亦或者通过将本文的思路框架扩展至**ESG事件驱动风险定价比较**？
