---
title: 多網站管理員與翻譯
description: 瞭解如何在專案中重複使用您的內容，以及在中管理多語言網站AEM。
translation-type: tm+mt
source-git-commit: 4fc4dbe2386d571fa39fd6d10e432bb2fc060da1
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# 多站點管理器和翻譯{#msm-and-translation}

Adobe Experience Manager的內建多網站管理員和翻譯工具可簡化內容本地化。

* Multi Site Manager(MSM)及其即時副本功能可讓您在多個位置使用相同的網站內容，同時允許變化：
   * [重複使用內容：多網站管理員和即時副本](msm/overview.md)
* 翻譯可讓您自動翻譯頁面內容，以建立和維護多語言網站：
   * [翻譯多語言網站的內容](translation/overview.md)

這兩項功能可結合，以符合[跨國和多語言](#multinational-and-multilingual-sites)的網站需求。

## 多國和多語言網站{#multinational-and-multilingual-sites}

您可以透過結合使用「多網站管理員」和翻譯工作流程，為跨國網站和多語言網站有效率地建立內容。

通常，您會以一種語言和特定國家／地區建立主體網站，然後視需要使用翻譯作為其他網站的基礎。

1. [將主](translation/overview.md) 版網站翻譯成不同的語言。
1. 使用[多站點管理器](msm/overview.md)可以：
   1. 重複使用主版網站及其翻譯的內容，為其他國家和文化建立網站。
   1. 視需要分離即時副本的元素，以新增本地化詳細資訊。

>[!TIP]
>
>將「多網站管理員」的使用限制在一種語言內。
>
>例如，使用英文主版為美國、加拿大、英國等地建立英文版頁面。 頁面，並使用法文母版為法國、瑞士、加拿大等地建立法文版頁面。

下圖說明主要概念的交集方式（但不顯示涉及的所有級別／元素）:

![本地化概觀](assets/localization-overview.png)

在這種情況下，MSM不會管理不同的語言版本。

* [](msm/overview.md) MSM管理從藍圖（即全域主版）到即時副本（即本機網站）的翻譯內容在語言界限內的部署。
* [translation](translation/overview.md)的整合功能與第AEM三方翻譯管理服務一起管理語言並將內容翻譯成這些不同的語言。

若是更進階的使用案例，MSM也可跨語言母版使用。

>[!TIP]
>
>針對所有使用案例，建議您閱讀下列最佳實務：
>
>* [MSM的最佳實務](msm/best-practices.md)
>* [翻譯的最佳做法](translation/best-practices.md)

