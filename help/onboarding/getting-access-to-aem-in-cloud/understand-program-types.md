---
title: 瞭解方案和方案類型
description: 瞭解方案和方案類型-Cloud Services
translation-type: tm+mt
source-git-commit: 5a4353cb31337882a1c13b0ed830ea64f617181a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 3%

---


# 了解方案和方案類型 {#understanding-programs}

在Cloud Manager中，您的最上層是「租用戶」實體，其中可包含多個「程式」。 每個方案只能包含一個以上的生產環境和多個非生產環境。

下圖顯示Cloud Manager中的實體階層。

![影像](assets/program-types1.png)

## 程式類型{#program-types}

用戶可以建立&#x200B;**沙盒**&#x200B;或&#x200B;**生產**&#x200B;程式。

* 建立&#x200B;*生產程式*以在將來的適當時間啟用即時通信。
如需詳細資訊，請參閱[生產程式簡介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-production-programs.md)。


* *沙盒程式*通常是為了提供訓練、執行示範、啟用、POC或說明檔案的目的而建立。 它不是要傳送即時流量，而且會有生產程式不會受到的限制。 它將包含網站和資產，並會自動填入Git分支，其中包含范常式式碼、開發環境和非生產管道。
如需詳細資訊，請參閱[沙盒程式簡介](/help/onboarding/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。

