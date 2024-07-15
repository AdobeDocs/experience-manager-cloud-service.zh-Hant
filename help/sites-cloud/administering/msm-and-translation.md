---
title: 多站點管理員和翻譯
description: 瞭解如何在您的專案中重複使用您的內容，並在AEM中管理多語言網站。
feature: Administering
role: Admin
exl-id: a3d48884-081e-44f8-8055-ee3657757bfd
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 3%

---

# 多站點管理員和翻譯 {#msm-and-translation}

Adobe Experience Manager的內建多網站管理員和翻譯工具可簡化內容的本地化工作。

* 多網站管理員(MSM)及其即時副本功能可讓您在多個位置使用相同的網站內容，同時允許以下變化：
   * [重複使用內容：多網站管理員和 Live Copy](msm/overview.md)
* 翻譯可讓您自動翻譯頁面內容，以建立和維護多語言網站：
   * [翻譯多語言網站的內容](translation/overview.md)

這兩個功能可以結合，以滿足[跨國和多語言](#multinational-and-multilingual-sites)網站的需求。

>[!TIP]
>
>如果您不熟悉翻譯內容，請參閱[網站翻譯歷程](/help/journey-sites/translation/overview.md)。 這是使用AEM強大翻譯工具翻譯AEM Sites內容的引導式方法；如果您沒有AEM或翻譯經驗，這是最理想的選擇。

## 跨國及多語言網站 {#multinational-and-multilingual-sites}

您可以透過結合使用多網站管理員和翻譯工作流程，有效率地建立跨國和多語言網站的內容。

通常，您會使用一種語言為特定國家/地區建立主要網站，然後將該內容作為其他網站的依據，並視需要使用翻譯。

1. [將](translation/overview.md)主要網站翻譯成其他語言。
1. 使用[多網站管理員](msm/overview.md)來：
   1. 重複使用主要網站的內容及其翻譯，為其他國家/地區和文化建立網站。
   1. 必要時，請分離即時副本的元素，以新增本地化詳細資訊。

>[!TIP]
>
>將多站點管理員的使用限製為使用一種語言的內容。
>
>例如，使用主要英文來建立美國、加拿大和英國頁面的英文版。 然後，使用主要法文版為法國、瑞士、加拿大等建立法文版頁面。

下圖說明主要概念如何交集（但並未顯示所有相關層級/元素）：

![本地化概觀](assets/localization-overview.png)

在此案例及可供比較的案例中，MSM不會據此管理不同的語言版本。

* [MSM](msm/overview.md)管理在語言範圍內從Blueprint （即主要全域）到即時副本（即本機網站）的翻譯內容部署。
* AEM的[翻譯](translation/overview.md)整合功能搭配協力廠商翻譯管理服務，可管理語言並將內容翻譯成這些不同的語言。

如需更進階的使用案例，MSM也可以跨主要語言使用。

>[!TIP]
>
>對於所有使用案例，建議閱讀以下最佳實務：
>
>* [MSM的最佳實務](msm/best-practices.md)
>* [翻譯最佳實務](translation/best-practices.md)
