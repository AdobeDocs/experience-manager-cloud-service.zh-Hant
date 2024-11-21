---
title: 重新整理多網站管理
description: 瞭解如何以重寫方式利用單一程式碼基底，以多語言網站設定專案的最佳實務建議。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: 02957fb8671d953a683ebd6e168979b11ad391c4
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---


# 重新整理多網站管理 {#repoless-msm}

本檔案假設您已為名為`my-aem-site`的專案建立基礎網站，且您想要使用AEM的MSM功能將其當地語系化。

如果您已經為重新定義的使用案例設定專案，則會將雲端設定指派到根頁面`/content/my-aem-site`的層級。 若為多語言網站，此組態指派必須變更至語言根，例如`/content/my-aem-site/language-master/de`。

