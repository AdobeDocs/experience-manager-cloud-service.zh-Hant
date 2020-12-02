---
title: 瞭解方案和方案類型
description: 瞭解方案和方案類型——雲端服務
translation-type: tm+mt
source-git-commit: 14da491cf09ed46ea425a8d65670d8b851aef388
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 3%

---


# 了解方案和方案類型 {#understanding-programs}

在Cloud Manager中，您的最上層是「租用戶」實體，其中可包含多個「程式」。  每個方案只能包含一個以上的生產環境和多個非生產環境。

下圖顯示Cloud Manager中的實體階層。

![影像](assets/program-types1.png)

## 程式類型{#program-types}

用戶可以建立&#x200B;**沙盒**&#x200B;或&#x200B;**規則**&#x200B;程式。

*沙盒*&#x200B;通常是為了提供訓練、執行示範、啟用、POC或說明檔案的目的而建立。 它不是要承載即時流量，而且會有常規程式所無法達到的限制。 它將包含網站和資產，並會自動填入Git分支，其中包含范常式式碼、開發環境和非生產管道。

建立一個&#x200B;*常規程式*，以便在將來的適當時間啟用即時通信。