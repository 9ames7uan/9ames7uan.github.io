---
layout: page
title: 母體至胎盤晶片陣列的流體驅動與快接界面開發
description: 團隊成員：賴彥錞、段鈞騰、江鎰丞、黃茂緯   指導教授：洪健中教授
img: assets/img/projects/Placenta/thumbnail.jpg
importance: 1
category: Work
related_publications: false
---

## 研究承起
本研究之發想，承啟實驗室模擬胎盤間腔內絨毛細胞的仿生晶片，繼而研究母體動脈與胎盤的模擬環境。

## 摘要
本研究建立 <font color="#ec7e42">仿生胎盤模型</font> 與電路控制的 <font color="#ec7e42">水泵系統</font>。透過 3D 建模技術構建胎盤模型，經流體模擬驗證結構，整合低通濾波、複合控制策略與感測器，模擬母體動脈至胎盤的血流傳輸、脈動，同時實現對流體參數的即時監控與控制，並支援 <font color="#ec7e42">胎盤器官晶片陣列</font> 的操作。

## 研究動機
母體生理狀況與胎兒健康的關聯一直是醫學焦點；然而，現有胎盤器官晶片多屬單一客製化設計，缺乏擴充彈性，反觀腎臟、肝臟及腸道等領域已成功實現晶片陣列化 [1]。

為突破此限制，本研究旨在開發具備 <font color="#ec7e42">快接介面</font> 的胎盤晶片陣列系統，並整合自動化水泵控制。透過此平台，我們不僅能解決多晶片操作的相容性問題，更能精確調控流入胎盤模型的血液參數。期透過此流體管理系統，為臨床上胎兒治療提供更具效率的體外模擬方案。

---

## 研究方法與步驟

為模擬實際胎盤運作情形，分成兩部分進行。第一部分為建立仿生胎盤模型，第二部分為模擬母體子宮動脈脈動，主要方法架構如圖一所示。

### 實驗架構

為模擬實際胎盤運作情形，分成兩部分進行，分別為為建立仿生胎盤模型、模擬母體子宮動脈脈動，主要方法架構如圖一所示。

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/System Structure.jpg" title="實驗方法架構圖" class="img-fluid rounded z-depth-1" caption="圖一：實驗方法架構圖" %}
    </div>
</div>

根據實驗架構，詳細步驟如下：

### 胎盤模型設計

<ol>
    <li class="mb-4">
        <strong>參數定義與模型規劃</strong>：搜尋胎盤生理參數（如直徑、厚度、總體積）及螺旋動脈之大小、數量與分佈，以此數據為基礎建立流體區域並決定模型設計方向。
        <div class="row justify-content-sm-center mt-3">
            <div class="col-sm-10">
                {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/Actual Placenta Cross-sectional.jpg" title="胎盤截面圖" class="img-fluid rounded z-depth-1" caption="圖二：胎盤截面圖" %}
            </div>
        </div>
    </li>

    <li class="mb-2">
        <strong>3D 幾何建模</strong>：使用 <font color="#ec7e42">Inventor</font> 繪圖軟體繪製胎盤之 3D 模型。
    </li>

    <li class="mb-2">
        <strong>流體力學模擬</strong>：將繪製完成的模型導入 <font color="#ec7e42">Ansys Fluent</font> 進行流體行為模擬。邊界條件設定為：輸入壓力 <font color="#ec7e42">85 mmHg</font>，輸出壓力 <font color="#ec7e42">0 mmHg</font>。
    </li>

    <li class="mb-4">
        <strong>結果驗證與製程決策</strong>：檢視模擬結果是否符合預期，並送交廠商進行 <font color="#ec7e42">3D 列印</font> 報價。
        <ul>
            <li>符合預算：執行實體列印。</li>
            <li>超出預算：建立簡化模型，並返回步驟 3 重新進行模擬驗證。</li>
        </ul>
    </li>
</ol>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/Placenta Model_1.jpg" title="胎盤模型圖" class="img-fluid rounded z-depth-1" caption="圖三：胎盤模型圖" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/Placenta Model_2.jpg" title="胎盤1/4簡化模型圖" class="img-fluid rounded z-depth-1" caption="圖四：胎盤1/4簡化模型圖（雙晶片）" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/Placenta Model_3.jpg" title="胎盤最簡化模型圖" class="img-fluid rounded z-depth-1" caption="圖五：胎盤最簡化模型圖（單晶片）" %}
    </div>
</div>
<div class="caption">
    橘色部分為 <font color="#ec7e42">Organ-on-Chip (OOC)</font> 預期放置處。
</div>

### 水泵流體系統

<ol>
    <li class="mb-4">
        <strong>硬體架構搭建</strong>：建立水泵迴路系統，硬體核心包含：
        <ul>
            <li>動力源：採用 <font color="#ec7e42">R385-12V 直流隔膜泵</font>。</li>
            <li>感測監控：選用 <font color="#ec7e42">ABPDANT005PGAA5 表壓感測器</font> 回授壓力數值。</li>
            <li>阻力模擬：利用 <font color="#ec7e42">球閥 (Ball Valve)</font> 的開度調整來模擬生理上的胎盤血管阻力。</li>
        </ul>
        <div class="row justify-content-sm-center mt-3">
            <div class="col-sm-10">
                {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/Pump System Structure.jpg" title="水泵系統架構圖" class="img-fluid rounded z-depth-1" caption="圖六：水泵流體系統架構圖" %}
            </div>
        </div>
    </li>

    <li class="mb-4">
        <strong>穩態實驗與閥門調校</strong>：為確認水泵出口壓力、流量及水閥開度三者間的耦合關係，我們先進行了穩態實驗。依據文獻數據，設定目標操作點為：
        <ul>
            <li>平均流量：$\approx 10 \text{ ml/s}$</li>
            <li>平均壓力：$\approx 1.6 \text{ psi}$</li>
        </ul>
        
        <div class="row mt-3">
            <div class="col-sm mt-3 mt-md-0">
                {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/7.jpg" title="不同電壓下，出口流量對水閥開度圖" class="img-fluid rounded z-depth-1" caption="圖七：不同電壓下，出口流量對水閥開度圖" %}
            </div>
            <div class="col-sm mt-3 mt-md-0">
                {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/8.jpg" title="不同電壓下，出口壓力對水閥開度圖" class="img-fluid rounded z-depth-1" caption="圖八：不同電壓下，出口壓力對水閥開度圖" %}
            </div>
        </div>
        <div class="row mt-3">
            <div class="col-sm mt-3 mt-md-0">
                {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/9.jpg" title="不同水閥開度下，出口流量對電壓圖" class="img-fluid rounded z-depth-1" caption="圖九：不同水閥開度下，出口流量對電壓圖" %}
            </div>
            <div class="col-sm mt-3 mt-md-0">
                {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/10.jpg" title="不同水閥開度下，出口壓力對電壓圖" class="img-fluid rounded z-depth-1" caption="圖十：不同水閥開度下，出口壓力對電壓圖" %}
            </div>
        </div>
        
        <p class="mt-2">經實驗比對關係圖後，將水閥鎖定於「<font color="#ec7e42">45° 開度</font>」，此時系統特性最符合真實胎盤阻力。</p>
    </li>

    <li class="mb-4">
        <strong>系統識別</strong>：在鎖定閥門（固定阻力）的條件下，進一步量測並繪製：
        <ul>
            <li>壓力 vs. 流量 (P-Q) 關係圖</li>
            <li>PWM vs. 壓力關係圖</li>
        </ul>

        <div class="row mt-3">
            <div class="col-sm mt-3 mt-md-0">
                {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/11.jpg" title="水泵出口壓力對流量圖、轉換方程式" class="img-fluid rounded z-depth-1" caption="圖十一：水泵出口壓力對流量圖、轉換方程式" %}
            </div>
            <div class="col-sm mt-3 mt-md-0">
                {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/12.jpg" title="輸入 PWM 對流量圖、轉換方程式" class="img-fluid rounded z-depth-1" caption="圖十二：輸入 PWM 對流量圖、轉換方程式" %}
            </div>
        </div>
        <p class="mt-2">將上述數據擬合成數學方程式，作為控制系統在線性範圍內的近似模型。</p>
    </li>

    <li class="mb-4">
        <strong>波形生成與單位轉換</strong>：控制目標設定為追蹤文獻中的生理流速波形。我們利用 <font color="#ec7e42">傅立葉級數 (Fourier Series)</font> 對文獻波形進行近似，以產生平滑的控制訊號。
        <br><br>
        已知子宮動脈口徑約為 $3.288 \text{ mm}$ (半徑 $r = 1.644 \text{ mm}$)，且輸入胎盤共有兩條子宮動脈，其流速 ($v$) 轉流量 ($Q$) 之關係式推導如下：

        $$
        \begin{aligned}
        Q(t) &= A \times v(t) \\
        \text{flow (ml/s)} &= 0.001 \times \pi \cdot 1.644^2 \times \text{flowrate (cm/s)} \times 10 \times 2
        \end{aligned}
        $$

        <div class="row mt-3">
            <div class="col-sm mt-3 mt-md-0">
                {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/13.jpg" title="文獻流速波形圖" class="img-fluid rounded z-depth-1" caption="圖十三：文獻流速波形圖" %}
            </div>
            <div class="col-sm mt-3 mt-md-0">
                {% include figure.liquid loading="eager" path="assets/img/projects/Placenta/14.jpg" title="擬合方程式重疊比較圖" class="img-fluid rounded z-depth-1" caption="圖十四：擬合方程式重疊比較圖" %}
            </div>
        </div>
    </li>
</ol>

### 水泵電路系統

由於水泵運作時會伴隨高頻雜訊干擾，對回授控制的精確度造成嚴重影響，因此本系統設計了一組 **四階 Sallen-Key 低通濾波器 (4th-order Sallen-Key Low-pass Filter)** 進行訊號調節。

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="lazy" path="assets/img/projects/Placenta/Circuit Structure.jpg" title="電路架構圖" class="img-fluid rounded z-depth-1" caption="圖十五：電路架構圖" %}
    </div>
</div>

<ol>
    <li class="mb-4">
        <strong>截止頻率範圍界定</strong>
        <p class="mt-2">
            根據生理訊號特徵（心跳週期 $0.7 \text{ s}$、8 次諧波、安全係數 $1.5$）與取樣定理（取樣頻率 $100 \text{ Hz}$），計算截止頻率 ($f_c$) 的上下限：
        </p>

        $$
        \begin{aligned}
        f_{c,min} &= \frac{1}{0.7} \times 8 \times 1.5 = 17.1 \text{ Hz} \\
        f_{c,max} &= \frac{100}{2} = 50 \text{ Hz}
        \end{aligned}
        $$

        <p>
            綜合考量後，本系統選定截止頻率為 $\color{#ec7e42}{f_c = 22.4 \text{ Hz}}$。對應之角頻率為：
        </p>
        $$
        \omega_c = 2\pi f_c \approx 140.74 \text{ rad/s}
        $$
    </li>

    <li class="mb-4">
        <strong>Sallen-Key 二階電路模型</strong>
        <p class="mt-2">
            本系統採用兩組二階 Sallen-Key 濾波器串聯以構成四階濾波效果，單一級 Sallen-Key 低通濾波器的輸入輸出關係如下：
        </p>

        $$
        \frac{V_o}{V_{in}} = \frac{\frac{1}{R_1 R_2 C_1 C_2}}{s^2 + \frac{(R_1 + R_2)C_2}{R_1 R_2 C_1 C_2}s + \frac{1}{R_1 R_2 C_1 C_2}}
        $$

        <p>
            為達到平坦通帶特性，採用 <font color="#ec7e42"><strong>Butterworth</strong></font> 濾波器設計準則。根據四階 Butterworth 多項式係數，系統之品質因數 ($Q$) 與特徵角頻率 ($\omega_c$) 關係式為：
        </p>

        $$
        \begin{aligned}
        Q &= \frac{\sqrt{R_1 R_2 C_1 C_2}}{(R_1+R_2)C_2} \\
        \omega_c &= \frac{1}{\sqrt{R_1 R_2 C_1 C_2}}
        \end{aligned}
        $$

        <p>兩級濾波器的目標 $Q$ 值分別計算得為 $1.3066$ 與 $0.5412$。</p>
    </li>

    <li class="mb-4">
        <strong>元件參數設計結果</strong>
        <p class="mt-2">
            依據上述 $Q$ 值與目標頻率 $f_c$，挑選匹配的電阻 ($R$) 與電容 ($C$) 組合如下：
        </p>

        <p><strong>第一級濾波器 (Stage 1)</strong></p>
        <ul>
            <li>選用元件：
                <ul>
                    <li>$R_1 = 67.4 \text{ k}\Omega, \quad R_2 = 48.275 \text{ k}\Omega$</li>
                    <li>$C_1 = 330 \text{ nF}, \quad C_2 = 47 \text{ nF}$</li>
                </ul>
            </li>
            <li>實際響應驗證：
                $$
                \begin{aligned}
                Q_1 &= \color{#ec7e42}{1.3066} \\
                \omega_c &= \color{#ec7e42}{140.767 \text{ rad/s}}
                \end{aligned}
                $$
            </li>
        </ul>

        <p><strong>第二級濾波器 (Stage 2)</strong></p>
        <ul>
            <li>選用元件：
                <ul>
                    <li>$R_3 = 200.56 \text{ k}\Omega, \quad R_4 = 78.75 \text{ k}\Omega$</li>
                    <li>$C_3 = 69 \text{ nF}, \quad C_4 = 47 \text{ nF}$</li>
                </ul>
            </li>
            <li>實際響應驗證：
                $$
                \begin{aligned}
                Q_2 &= \color{#ec7e42}{0.5452} \\
                \omega_c &= \color{#ec7e42}{139.727 \text{ rad/s}}
                \end{aligned}
                $$
            </li>
        </ul>
    </li>

    <li class="mb-4">
        <strong>濾波成效驗證</strong>
        <p class="mt-2">
            經實驗量測，比較「無濾波」、「一階濾波」與「四階濾波」之訊號表現，結果如下表所示。數據顯示四階濾波器能顯著降低峰對峰值 (Vpp)，並將主要雜訊頻率移至高頻區以便濾除，有效提升訊號信噪比 (SNR)。
        </p>

        <div class="table-responsive">
            <table class="table table-striped table-hover">
                <thead>
                    <tr>
                        <th style="text-align: left;">濾波階段</th>
                        <th style="text-align: center;">雜訊主頻率 (Hz)</th>
                        <th style="text-align: center;">峰對峰值 (mV)</th>
                        <th style="text-align: center;">改善幅度</th>
                    </tr>
                </thead>
                <tbody>
                    <tr>
                        <td style="text-align: left;">無濾波</td>
                        <td style="text-align: center;">64.516</td>
                        <td style="text-align: center;">616</td>
                        <td style="text-align: center;">-</td>
                    </tr>
                    <tr>
                        <td style="text-align: left;">一階濾波</td>
                        <td style="text-align: center;">64.516</td>
                        <td style="text-align: center;">204</td>
                        <td style="text-align: center;">66.8%</td>
                    </tr>
                    <tr>
                        <td style="text-align: left;"><strong>四階濾波</strong></td>
                        <td style="text-align: center;">234.7</td>
                        <td style="text-align: center;"><strong>94</strong></td>
                        <td style="text-align: center;"><font color="#ec7e42"><strong>84.7%</strong></font></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </li>
</ol>

### 水泵控制系統

由於本系統之控制首要目標為確保「波形形狀」與目標生理波形高度吻合，且對於訊號相位延遲 (Phase Delay) 具有一定的容許度，因此採用 <font color="#ec7e42">前饋控制 (Feedforward Control)</font> 為主、<font color="#ec7e42">積分控制 (Integral Control)</font> 為輔的複合控制策略。

此外，考量水泵在不同 PWM 輸出區間（特別是低佔空比與高佔空比區域）表現出顯著的非線性差異，單一增益參數無法滿足全域控制需求。為此，本研究導入 <font color="#ec7e42">分段增益排程法 (Gain Scheduling)</font>，將操作範圍劃分為不同區段，並針對各區段設定獨立的積分增益值 ($K_i$)，以達成最佳化控制效果。

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="lazy" path="assets/img/projects/Placenta/Control Structure.jpg" title="控制系統架構圖" class="img-fluid rounded z-depth-1" caption="圖十六：控制系統架構圖" %}
    </div>
</div>

---

## 結果與討論

1. 流體模擬結果
模擬顯示流體可如預期在模型中流通，並成功分流至 OOC 區域，流速等級符合生理條件（毫米級）。

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/17.jpg" title="原模型流速圖" class="img-fluid rounded z-depth-1" caption="圖十七、原模型流速圖" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig17.jpg" title="1/4模型流速圖" class="img-fluid rounded z-depth-1" caption="圖十八、1/4模型流速圖" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig18.jpg" title="最簡模型流速圖" class="img-fluid rounded z-depth-1" caption="圖十九、最簡模型流速圖" %}
    </div>
</div>

2. 濾波降噪成效
使用四階濾波後，訊號峰對峰值 (Vpp) 顯著下降，有效濾除高頻雜訊。

| 濾波階段 | 雜訊主頻率 (Hz) | 峰對峰值 (mV) |
| :--- | :---: | :---: |
| 無濾波 | 64.516 | 616 |
| 一階濾波 | 64.516 | 204 |
| **四階濾波** | **234.7** | **94** |

3. 波形追蹤結果
加入回授控制與增益排程後，實際量測波形與目標生理波形高度吻合。

<div class="row">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="lazy" path="assets/img/projects/Placenta/20.jpg" title="濾波前追蹤狀況重疊圖" class="img-fluid rounded z-depth-1" caption="圖二十、濾波前追蹤狀況重疊圖" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="lazy" path="assets/img/projects/Placenta/21.jpg" title="無回授控制系統追蹤狀況重疊圖" class="img-fluid rounded z-depth-1" caption="圖二十、無回授控制系統追蹤狀況重疊圖" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid loading="lazy" path="assets/img/projects/Placenta/22.jpg" title="回授控制系統追蹤狀況重疊圖" class="img-fluid rounded z-depth-1" caption="圖二十、回授控制系統追蹤狀況重疊圖" %}
    </div>
</div>

**最終脈動參數比較：**

| 參數 | 目標波形 | 量測波形 | 誤差 (%) |
| :--- | :---: | :---: | :---: |
| PS (收縮峰值速度 cm/s) | 82.31 | 81.33 | 1.19 |
| ED (舒張末期速度 cm/s) | 48.97 | 46.92 | 4.19 |
| M (平均流速) | 58.89 | 59.00 | 0.19 |
| PI (脈動指數) | 0.566 | 0.583 | 3.04 |
| RI (阻力指數) | 0.405 | 0.423 | 4.47 |

---

## 結論
胎盤模型之流體模擬顯示出其結構與實際胎盤接近，而水泵模擬則與血流脈動相符，兩者皆與預期相符，後續若有經費，則會將模型印出，與水泵結合，形成一完整系統。

---

## 參考文獻
1. H. Azizgolshani et al. (2021) High-throughput organ-on-chip platform... *Lab on a Chip*.
2. Sarah K Griffiths et al. (2014) Placental structure, function and drug transfer.
3. Chernyavsky IL et al. (2010) A mathematical model of intervillous blood flow.
4. Sciscione, A. C., & Hayes, E. J. (2009). Uterine artery Doppler flow studies.