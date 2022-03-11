---
title: 多站點管理器和翻譯
description: 瞭解如何在項目中重複使用您的內容以及管理中的多語言網AEM站。
feature: Administering
role: Admin
exl-id: a3d48884-081e-44f8-8055-ee3657757bfd
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 多站點管理器和翻譯 {#msm-and-translation}

Adobe Experience Manager的內置多站點管理器和翻譯工具簡化了內容本地化。

* 多站點管理器(MSM)及其Live Copy功能使您能夠在多個位置使用相同的站點內容，同時允許以下變化：
   * [重新使用內容：多站點管理器和即時拷貝](msm/overview.md)
* 翻譯允許您自動翻譯頁面內容以建立和維護多語言網站：
   * [翻譯多語言站點的內容](translation/overview.md)

這兩個功能可以結合起來，以滿足同時兼有這兩個功能的網站 [多語種](#multinational-and-multilingual-sites)。

>[!TIP]
>
>如果您是翻譯內容的新手，請參閱我們的 [網站翻譯之旅，](/help/journey-sites/translation/overview.md) 它是指通過使用功能強大的翻譯工具AEM翻譯您的AEM Sites內容的指導路AEM徑，是那些沒有翻譯經驗的人的理想選擇。

## 跨國和多語言站點 {#multinational-and-multilingual-sites}

您可以通過「多站點管理器」和翻譯工作流的組合使用，高效地為跨國和多語言站點建立內容。

通常，您會以一種語言和特定國家（地區）建立主體站點，然後根據需要使用翻譯將該內容用作其他站點的基礎。

1. [翻譯](translation/overview.md) 把主體網站翻譯成不同的語言。
1. 使用 [多站點管理器](msm/overview.md) 至：
   1. 重新使用主體站點及其翻譯的內容，為其他國家和文化建立站點。
   1. 如果需要，分離即時副本的元素以添加本地化詳細資訊。

>[!TIP]
>
>將多站點管理器的使用限制為使用一種語言的內容。
>
>例如，使用英文母版為美國、加拿大、英國等建立英文版頁。 頁面，並使用法文母版為法國、瑞士、加拿大等建立法文版本的頁面。

下圖說明了主要概念如何相交（但不顯示涉及的所有級別/元素）:

![本地化概述](assets/localization-overview.png)

在這種情況下，以及可比較的情況下，MSM不會管理這樣的不同語言版本。

* [MSM](msm/overview.md) 管理在語言邊界內將已翻譯內容從藍圖（即全局主資料）部署到即時拷貝（即本地站點）。
* 的 [翻譯](translation/overview.md) 與第AEM三方翻譯管理服務一起管理這些語言並將內容翻譯成這些不同語言的整合能力。

對於更高級的使用情形，MSM也可跨語言母版使用。

>[!TIP]
>
>對於所有使用情形，建議閱讀以下最佳做法：
>
>* [MSM的最佳做法](msm/best-practices.md)
>* [翻譯最佳做法](translation/best-practices.md)

