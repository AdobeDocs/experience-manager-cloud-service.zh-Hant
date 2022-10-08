---
title: 多站點管理員和翻譯
description: 了解如何在專案中重複使用內容，以及在AEM中管理多語言網站。
feature: Administering
role: Admin
exl-id: a3d48884-081e-44f8-8055-ee3657757bfd
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# 多站點管理員和翻譯 {#msm-and-translation}

Adobe Experience Manager內建的多網站管理員和翻譯工具可簡化內容本地化的流程。

* Multi Site Manager(MSM)及其Live Copy功能可讓您在多個位置中使用相同的網站內容，同時允許變數：
   * [重複使用內容：多網站管理員和即時副本](msm/overview.md)
* 翻譯可讓您自動翻譯頁面內容，以建立和維護多語言網站：
   * [轉譯多語言網站的內容](translation/overview.md)

這兩項功能可結合，以迎合同時兼顧的網站需求 [多語種](#multinational-and-multilingual-sites).

>[!TIP]
>
>如果您是初次翻譯內容，請參閱 [網站翻譯歷程，](/help/journey-sites/translation/overview.md) 這是使用AEM功能強大的翻譯工具來轉譯您的AEM Sites內容的引導式路徑，最適合沒有AEM或翻譯體驗的人。

## 跨國和多語言網站 {#multinational-and-multilingual-sites}

您可以結合使用「多網站管理員」和翻譯工作流程，以有效建立跨國和多語言網站的內容。

通常，您會以一種語言和特定國家/地區建立主網站，然後視需要使用翻譯，將該內容作為其他網站的基礎。

1. [翻譯](translation/overview.md) 將主版網站改成不同語言。
1. 使用 [多網站管理員](msm/overview.md) 至：
   1. 從主網站及其翻譯中重複使用內容，為其他國家和文化建立網站。
   1. 如果需要，請分離Live Copy的元素以添加本地化詳細資訊。

>[!TIP]
>
>將多網站管理員的使用限制為一種語言的內容。
>
>例如，使用英文主版為美國、加拿大、英國等建立英文版頁面。 頁面，並使用法文主版為法國、瑞士、加拿大等建立法文版頁面。

下圖說明主要概念如何交叉（但不顯示涉及的所有級別/元素）:

![本地化概述](assets/localization-overview.png)

在此及可比較的情況下，MSM不會管理這樣的不同語言版本。

* [MSM](msm/overview.md) 在語言的邊界內管理從Blueprint（即全局主版）到Live Copy（即本地站點）的翻譯內容的部署。
* 此 [翻譯](translation/overview.md) AEM的整合功能與第三方翻譯管理服務相結合，可管理語言並將內容翻譯成這些不同語言。

如需更進階的使用案例，MSM也可跨語言主版使用。

>[!TIP]
>
>針對所有使用案例，建議閱讀下列最佳實務：
>
>* [MSM最佳實務](msm/best-practices.md)
>* [翻譯最佳實務](translation/best-practices.md)

