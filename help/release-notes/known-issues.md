---
title: 已知問題
description: Adobe Experience Manager as a Cloud Service 已知問題
exl-id: 897b944a-d320-4d21-91f4-2cd3da6179b1
source-git-commit: 755c0072148ad73486df2ccfed69248b9d73ec2a
workflow-type: ht
source-wordcount: '177'
ht-degree: 100%

---

# 已知問題 {#known-issues}

本文列出 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 產品的已知問題。 此清單會隨著 [!DNL Experience Manager] 推出各個版本而持續修訂和更新。

如需已知問題的詳細資訊，請[連絡支援團隊](https://experienceleague.adobe.com/?lang=en&amp;support-solution=Experience+Manager#support)。

<!-- 
## Platform {#platform}
-->

## Sites {#sites}

[!DNL Sites] 中部分已知問題包括：

* 在 GraphQL IDE 中，您可以[管理持續性查詢的快取](/help/headless/graphql-api/graphiql-ide.md##managing-cache)。
   * 在第一次儲存時，為標題儲存的值會設定為`0` (而不是預設值) - 如果使用者沒有在對話框中變更這些值。
   * 後續進行的儲存會正確儲存值。
   * 因此，使用者必須儲存標題兩次。

## [!DNL Assets] {#assets}

<!-- Jira label: assets-cloud-known-issues -->

[!DNL Assets] 中部分已知問題包括：

* **下載**：如果您下載一個空白資料夾，[!DNL Experience Manager] 會傳達一則關於建立 ZIP 封存檔的成功訊息，但並沒有建立封存檔。

* **中繼資料結構**：資產評等工具集會造成 JSP 編譯錯誤。該工具已從中繼資料結構中移除。<!-- CQ-4282865, CQ-4284633 -->

另外，請參閱[ [!DNL Experience Manager Assets]](/help/assets/assets-cloud-changes.md) 重大變更。

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
>* [ [!DNL Experience Manager]](aem-cloud-changes.md) 重大變更
>* [過時和移除的功能](deprecated-removed-features.md)
>* [發行說明](home.md)

