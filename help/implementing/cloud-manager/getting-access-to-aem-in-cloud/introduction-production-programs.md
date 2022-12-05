---
title: 生產計劃簡介
description: 了解什麼是生產程序以及如何設定您的計劃的建議。
exl-id: bb8d4a5a-b26a-4718-9327-149fedb87e6a
source-git-commit: a6152a1529b5c70bcf056857204e7ff97fc614e4
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 100%

---


# 生產計劃簡介 {#production-programs}

生產程序適用於準備開始編寫、構建和測試計劃碼的團隊，目標是部署它以託管實時流量。

在你之後[建立您的生產程序，](creating-production-programs.md)一個[程序建立嚮導](using-the-wizard.md)根據使用者建立程序的目標，引導使用者進行選擇。

## 程序建立選項 {#program-creation-options}

您與 Adobe 的合約協議定義了您的特定組織在建立製作程序時可用的解決方案的數量和類型。您可以控制如何將可用解決方案映射到 Cloud Manager 程序。

下表描述了可用解決方案的常見場景以及基於它們建立的典型生產程序。

| 可用的解決方案 | 計劃選項 | 包括什麼 | 使用時機 | 範例 |
|--- |--- |--- |--- |---|
| 1 Sites 解決方案 | 建立 1 Sites 專用計劃 | 1 生產 + 1 階段、1 開發 | N/A | 不適用 |
| 1 Assets 解決方案 | 建立 1 Assets 專用計劃 | 1 生產 + 1 階段、1 開發 | 不適用 | 不適用 |
| 1 個 Sites +1 個 Assets | 建立一個計劃：<br> 1 Sites &amp; Assets 計劃 | 1 生產 + 1 階段、2 開發 | 當大多數數位資產用於支援網站實施時。<br>在這種情況下，大多數數位資產都處於完成狀態，可以透過 Sites 用於跨渠道體驗。<br>通常，一個團隊負責管理 Sites 和 Assets 的內容。 | 主要用於網站的圖像。<br>將透過 AEM Sites 中內建的內部入口網站分發的 PDF。 |
| 1 個 Sites +1 個 Assets | 建立獨立的計劃：<br>僅 1 個 Sites 計劃和僅 1 個 Assets 計劃 | 1 生產 + 1 階段，1 開發<br>1 生產 + 1 階段，1 開發 | 當許多數位資產不直接支援網站實施時。<br>在這種情況下，資產處於各種狀態，包括原始文件類型和正在進行的工作。<br>一個專門的創意團隊透過其自己的生命週期管理數位資產，並且具有與 Sites 內容管理團隊不同的工作流程和發布週期。 | 照片拍攝的原始圖像存儲在 Assets 程序中，只有少數幾個將用於 Sites 實施。<br>大量 Creative Cloud 文件類型 (如 Photoshop 和 Illustrator) 在 AEM Assets 中進行管理，並在生成完成的資源之前透過自己的核准工作流程。<br>考慮在這種情況下使用[關聯 Assets](/help/assets/use-assets-across-connected-assets-instances.md#overview-of-connected-assets)。 |
| 1 個 Sites + 1 個 Sites | 建立獨立的計劃：<br>僅 1 個 Sites 和僅 1 個 Sites 計劃 | 1 生產 + 1 階段，1 開發<br>1 生產 + 1 階段，1 開發 | 對於多租使用者網站實施。<br>在這種情況下，必須管理具有自己的發布計劃和專門的開發和內容團隊的多個網站。 | 兩個擁有專門網站和獨立開發團隊的零售品牌 |

>[!NOTE]
>
>[不能編輯和刪除](editing-programs.md)生產計畫。
