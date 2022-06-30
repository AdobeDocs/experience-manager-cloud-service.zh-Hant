---
title: 已知問題
description: 已知的Adobe Experience Manager as a Cloud Service問題
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 755c0072148ad73486df2ccfed69248b9d73ec2a
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 21%

---

# 已知問題 {#known-issues}

本文列出了 [!DNL Adobe Experience Manager] 作為 [!DNL Cloud Service] 提供。 該清單將隨每次連續發佈的 [!DNL Experience Manager]。

如需已知問題的詳細資訊，請[連絡支援團隊](https://experienceleague.adobe.com/?lang=en&amp;support-solution=Experience+Manager#support)。

<!-- 
## Platform {#platform}
-->

## Sites {#sites}

中的一些已知問題 [!DNL Sites] 為：

* 在GraphQL IDE中，您可以 [管理永續查詢的快取](/help/headless/graphql-api/graphiql-ide.md##managing-cache)。
   * 在第一次保存時，為標題保存的值將設定為 `0` （而不是預設值） — 如果用戶未更改對話框中的這些值。
   * 在後續保存時，值會正確保存。
   * 因此，用戶必須保存兩次頭。

## [!DNL Assets] {#assets}

<!-- Jira label: assets-cloud-known-issues -->

中的一些已知問題 [!DNL Assets] 為：

* **下載**:如果下載了空資料夾， [!DNL Experience Manager] 傳達了有關建立ZIP存檔的成功消息，但未建立存檔。

* **中繼資料結構**：資產評等工具集會造成 JSP 編譯錯誤。該工具已從中繼資料結構中移除。<!-- CQ-4282865, CQ-4284633 -->

另請參見 [顯著更改 [!DNL Experience Manager Assets]](/help/assets/assets-cloud-changes.md)。

<!-- This content was added at GA. Not sure if we should continue to have this commitment about upcoming features/enh. in the docs. Commenting it for now.

### Upcoming Assets capabilities {#upcoming-assets-capabilities}

A few capabilities of Adobe Experience Manager Assets that depend on foundation capabilities, which are not yet available in the Experience Manager as a Cloud Service deployment architecture, are expected to be enabled at a later stage:

* Capabilities not enabled at this stage due to dependency on Commerce Integration Framework APIs:
  * Photoshoot workflow models.
  * Product information tab in the asset properties user interface is not populated.

* Capabilities not enabled at this stage due to dependency on InDesign Server integration:
  * Asset Templates and Asset Catalogs.
  * Multi-page preview of Adobe InDesign files.
-->

>[!MORELIKETHIS]
>
>* [主要變動 [!DNL Experience Manager]](aem-cloud-changes.md)
>* [過時和移除的功能](deprecated-removed-features.md)
>* [發行說明](home.md)

