---
title: 已知問題
description: Adobe Experience Manager as a Cloud Service的已知問題
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 8ec0ce3425e7cade0a6774a4452d4f47ab971375
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 33%

---

# 已知問題 {#known-issues}

本文列出 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 提供。 此清單會隨著 [!DNL Experience Manager].

如需已知問題的詳細資訊，請[連絡支援團隊](https://experienceleague.adobe.com/?lang=en&amp;support-solution=Experience+Manager#support)。

<!-- 
## Platform {#platform}

## Sites {#sites}
-->

## [!DNL Assets] {#assets}

<!-- Jira label: assets-cloud-known-issues -->

中的一些已知問題 [!DNL Assets] 為：

* **下載**:如果下載空資料夾， [!DNL Experience Manager] 會傳達關於建立ZIP封存的成功訊息，但不會建立封存。

* **中繼資料結構**：資產評等工具集會造成 JSP 編譯錯誤。該工具已從中繼資料結構中移除。<!-- CQ-4282865, CQ-4284633 -->

另請參閱 [重大變更 [!DNL Experience Manager Assets]](/help/assets/assets-cloud-changes.md).

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
>* [重大變更 [!DNL Experience Manager]](aem-cloud-changes.md)
>* [過時和移除的功能](deprecated-removed-features.md)
>* [發行說明](home.md)

