---
layout: page
title: project 4
description: 結合仿生胎盤模型與自動化流體控制，模擬母體至胎兒的血流傳輸機制
img: assets/img/projects/placenta/thumbnail.jpg
importance: 1
category: Fun
related_publications: false
---

本研究旨在建立仿生胎盤模型與電路控制的水泵系統。透過 3D 建模技術構建胎盤模型，經流體模擬驗證結構，整合低通濾波、複合控制策略與感測器，模擬母體動脈至胎盤的血流傳輸與脈動。

### 研究動機
母體生理狀況與胎兒健康的關聯一直是醫學焦點；然而，現有胎盤器官晶片多屬單一客製化設計，缺乏擴充彈性。本研究開發具備快接介面的胎盤晶片陣列系統，並整合自動化水泵控制，解決多晶片操作的相容性問題，更能精確調控流入胎盤模型的血液參數，為臨床上胎兒治療提供更具效率的體外模擬方案。

---

### 研究方法

為模擬實際胎盤運作情形，本研究分為「建立仿生胎盤模型」與「模擬母體子宮動脈脈動」兩大部分。

#### 1. 實驗架構

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/placenta/fig1.jpg" title="實驗方法架構圖" class="img-fluid rounded z-depth-1" caption="圖一、實驗方法架構圖" %}
    </div>
</div>

#### 2. 胎盤模型設計 (CFD 模擬)
利用 Inventor 繪製胎盤模型，並導入 Ansys Fluent 進行流體行為模擬（輸入壓力 85mmHg，輸出 0mmHg）。針對預算與製造可行性，我們設計了從完整到簡化的多種模型。

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig3.jpg" title="未簡化模型" class="img-fluid rounded z-depth-1" caption="圖三、未簡化胎盤模型" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig4.jpg" title="1/4簡化模型" class="img-fluid rounded z-depth-1" caption="圖四、1/4簡化模型（雙晶片）" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig5.jpg" title="最簡化模型" class="img-fluid rounded z-depth-1" caption="圖五、最簡化模型（單晶片）" %}
    </div>
</div>
<div class="caption">
    橘色部分為 Organ-on-Chip (OOC) 預期放置處。
</div>

#### 3. 水泵流體與電路系統
採用 R385-12V 直流隔膜泵搭配 ABPDANT005PGAA5 表壓感測器。為解決水泵雜訊，設計了四階 Sallen-key 低通濾波器 (Cut-off frequency $f_c = 22.4 Hz$)。

<div class="row">
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig6.jpg" title="水泵系統架構" class="img-fluid rounded z-depth-1" caption="圖六、水泵系統架構" %}
    </div>
    <div class="col-sm-6 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig14.jpg" title="完整電路架構圖" class="img-fluid rounded z-depth-1" caption="圖十四、完整濾波電路架構圖" %}
    </div>
</div>

#### 4. 控制策略
控制目標為模擬文獻中的子宮動脈流速波形。採用**前饋控制 (Feedforward)** 為主、**積分控制 (Integral)** 為輔的策略，並引入**分段增益排程 (Gain Scheduling)** 來處理水泵在不同 PWM 區間的非線性特性。

<div class="row justify-content-sm-center">
    <div class="col-sm-10 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig15.jpg" title="完整控制架構圖" class="img-fluid rounded z-depth-1" caption="圖十五、完整控制架構圖" %}
    </div>
</div>

---

### 結果與討論

#### 1. 流體模擬結果
模擬顯示流體可如預期在模型中流通，並成功分流至 OOC 區域，流速等級符合生理條件（毫米級）。

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig16.jpg" title="原模型流速圖" class="img-fluid rounded z-depth-1" caption="圖十六、原模型流速圖" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig17.jpg" title="1/4模型流速圖" class="img-fluid rounded z-depth-1" caption="圖十七、1/4模型流速圖" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig18.jpg" title="最簡模型流速圖" class="img-fluid rounded z-depth-1" caption="圖十八、最簡模型流速圖" %}
    </div>
</div>

#### 2. 濾波降噪成效
使用四階濾波後，訊號峰對峰值 (Vpp) 顯著下降，有效濾除高頻雜訊。

| 濾波階段 | 雜訊主頻率 (Hz) | 峰對峰值 (mV) |
| :--- | :---: | :---: |
| 無濾波 | 64.516 | 616 |
| 一階濾波 | 64.516 | 204 |
| **四階濾波** | **234.7** | **94** |

#### 3. 波形追蹤結果
加入回授控制與增益排程後，實際量測波形與目標生理波形高度吻合。

<div class="row">
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig19.jpg" title="濾波前" class="img-fluid rounded z-depth-1" caption="圖十九、濾波前雜訊" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig20.jpg" title="無回授" class="img-fluid rounded z-depth-1" caption="圖二十、無回授控制" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/placenta/fig21.jpg" title="回授控制" class="img-fluid rounded z-depth-1" caption="圖二十一、回授控制結果" %}
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

### 結論
胎盤模型之流體模擬顯示出其結構與實際胎盤接近，而水泵模擬則與血流脈動相符，兩者皆與預期相符，後續若有經費，則會將模型印出，與水泵結合，形成一完整系統。

---

### 參考文獻
1. H. Azizgolshani et al. (2021) High-throughput organ-on-chip platform... *Lab on a Chip*.
2. Sarah K Griffiths et al. (2014) Placental structure, function and drug transfer.
3. Chernyavsky IL et al. (2010) A mathematical model of intervillous blood flow.
4. Sciscione, A. C., & Hayes, E. J. (2009). Uterine artery Doppler flow studies.