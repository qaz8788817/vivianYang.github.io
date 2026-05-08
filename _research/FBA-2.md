---
layout: single
title: "dMRI技術專欄(2)：解構 FBA 實作流程——從數據預處理到統計分析"
# collection: research
topic: FBA
excerpt: "深入探討 MRtrix3 中的 FBA 運算流程，以及如何透過 CFE 統計方法挖掘具備生物意義的顯著差異。"
header:
  teaser: /assets/images/about_me_banner.jpg
author_profile: true
toc: true
toc_label: "實作流程索引"
toc_icon: "microchip"
toc_sticky: true
---

### 引言
在上一篇中，我們理解了FBA如何透過Fixel單位破解纖維交叉的困境。  
然而，要從一堆雜亂的擴散訊號中提取出FD、FC與FDC，需要經過嚴謹的運算流程。  
本篇將帶領大家走進實驗室，拆解基於MRtrix3框架下的FBA實作邏輯。

### 1. 預處理：數據質量的生命線
在進入FBA之前，數據必須經過一系列去雜訊與校正，  
這決定了後續FOD(Fiber Orientation Distribution)的可靠性。  
* **Denoising & Gibbs Unringing**：消除熱噪訊與影像邊緣的震盪偽影。  
* **Motion & Eddy Current Correction**：校正掃描時的頭部晃動與渦流效應。  
* **Bias Field Correction**：修正磁場不均勻造成的強度偏差。  

### 2. 建立「大腦地圖」：群體模板 (Population Template)
FBA 的分析是在一個共同空間進行的。  
不同於 DTI 常用現成的 MNI 模板，FBA 傾向於建立一個 **Study-specific Population Template**。
* **為什麼要自建模板？**   
因為每個研究的受試對象(如中風患者 vs. 健康對照組)大腦形態差異極大，  
使用所有受試者影像生成的平均模板，能更精確地對齊纖維走向，減少Registration誤差。  

<div style="background-color: #f9f9f9; padding: 20px; border-radius: 10px; margin: 20px 0; text-align: center;">
  <img src="{{ '/assets/images/FBA/FBA(2)/wmfod_template.png' | relative_url }}" 
       alt="Population Template 示意圖" 
       style="max-width: 100%; height: auto; border: 1px solid #ddd;">
  <p style="font-size: 0.9em; color: #666; margin-top: 10px;">
    <i>圖：受試者的群體模板示意圖。</i>
  </p>
</div>

### 3. 核心統計：CFE (Connectivity-based Fixel Enhancement)
得到每個Fixel的指標後，我們如何判斷兩組人間的差異是否具備統計學意義？  
FBA使用的是專為纖維設計的 **CFE** 方法。  

* **空間連通性**：與傳統像素級統計不同，CFE會考慮纖維的 *Connectivity*。  
如果某個Fixel出現差異，且與它沿著同一條路徑相連的Fixel也顯示出差異，CFE會增強該區域的顯著性。  
* **多重比較校正**：通常配合 **FWE (Family-wise Error)** 校正。
  * *註：在臨床研究中，若 FWE 校正後無顯著結果，有時會觀察 $p < 0.001$ (Uncorrected) 的傾向，這對於探索性研究（如臨床預後關聯）仍具參考價值。*

### 4. 結果解讀：方向特異性的視覺化
當我們在統計圖上看到顯著變化的區域時，  
FBA讓我們能說出：「這是在皮質脊髓束 (CST) 上，且是往某個特定方向的纖維發生了 FD 下降。」  

### 5. 結語：從影像到臨床的橋樑
FBA不僅是數學上的進步，更是臨床解釋的突破。透過 FD 與 FC 的分離，我們能區分受試者是處於神經退化的「早期軸突流失」還是「晚期形態萎縮」。

在我的碩士論文研究中，使用了VBA、FBA以及NODDI等影像指標，結合機器學習的特徵重要性分析，進而使模型準確率提升。  
希望這兩篇介紹能讓大家對這項技術有更清晰的輪廓！  
