---
title: 瞭解方案和方案類型
description: 瞭解方案和方案類型——雲端服務
translation-type: tm+mt
source-git-commit: 14da491cf09ed46ea425a8d65670d8b851aef388

---


# 了解方案和方案類型 {#understanding-programs}

在Cloud manager中，您的最上層是「租用戶」實體，其中可包含多個「程式」。  每個方案只能包含一個以上的生產環境和多個非生產環境。

下圖顯示Cloud manager中的實體階層。

![影像](assets/program-types1.png)

## 方案類型 {#program-types}

使用者可以建立沙 **箱** 或 **Regular程式** 。

建 *立沙盒* ，通常是為了提供訓練、執行示範、啟用、POC或檔案的目的。 它不是要承載即時流量，而且會有常規程式所無法達到的限制。 它將包含網站和資產，並會自動填入Git分支，其中包含范常式式碼、開發環境和非生產管道。

我們 *會建立一個* 「常規」計畫，以便在未來適當的時間啟用即時流量。