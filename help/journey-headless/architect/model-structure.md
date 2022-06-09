---
title: 瞭解在中建立內容片段模型AEM
description: 瞭解使用內容片段模型為無頭CMS建模內容的概念和機制。
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
source-git-commit: c25bdab65a742e8ffc3a1579474f4589e04abce9
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 3%

---

# 瞭解在中建立內容片段模型AEM {#architect-headless-content-fragment-models}

## 到目前為止的故事 {#story-so-far}

在 [無AEM頭內容作者之旅](overview.md) 這樣 [無頭內容建模基礎知識AEM](basics.md) 介紹了與無頭創作相關的基本概念和術語。

本文基於這些內容，以便您瞭解如何為無頭項目建立您自己的內容AEM片段模型。

## 目標 {#objective}

* **觀眾**:初學者
* **目標**:使用內容片段模型為無頭CMS建模內容的概念和機制。

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools -> General -> Configuration Browser. You can either select to configure the global entry, or create a new configuration. For example:

![Define configuration](/help/assets/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## 建立內容片段模型 {#creating-content-fragment-models}

然後可以建立內容片段模型並定義結構。 可以在 **工具** -> **常規** -> **內容片段模型**。

![工具中的內容片段模型](assets/cfm-tools.png)

選擇此選項後，導航到模型的位置並選擇 **建立**。 您可以在此處輸入各種密鑰詳細資訊。

選項 **啟用模型** 預設情況下激活。 這意味著您的模型在保存後即可供使用（在建立內容片段時）。 如果需要，可以取消激活此功能 — 以後有啟用（或禁用）現有模型的機會。

![建立內容片段模型](/help/assets/content-fragments/assets/cfm-models-02.png)

確認 **建立** 你可以 **開啟** 定義結構的模型。

## 定義內容片段模型 {#defining-content-fragment-models}

首次開啟新模型時，您將看到 — 左邊有一個大的空白區域，以及 **資料類型** 右邊：

![空模型](/help/assets/content-fragments/assets/cfm-models-03.png)

那麼，我們該怎麼辦？

可以拖動 **資料類型** 到左邊的空間 — 你已經在定義模型了！

![定義欄位](/help/assets/content-fragments/assets/cfm-models-04.png)

添加資料類型後，將需要定義 **屬性** 那塊地。 這取決於所使用的類型。 例如：

![資料屬性](/help/assets/content-fragments/assets/cfm-models-05.png)

您可以根據需要添加任意多個欄位。 例如：

![內容片段模型](/help/assets/content-fragments/assets/cfm-models-07.png)

### 您的內容作者 {#your-content-authors}

您的內容作者看不到您用於建立模型的實際資料類型和屬性。 這意味著您可能必須提供有關它們如何完成特定欄位的幫助和資訊。 有關基本資訊，您可以使用「欄位標籤」和「預設值」，但更複雜的情況可能需要考慮項目特定文檔。

>[!NOTE]
>
>請參閱其他資源 — 內容片段模型。

## 管理內容片段模型 {#managing-content-fragment-models}

<!-- needs more details -->

管理內容片段模型涉及：

* 啟用（或禁用）它們 — 這使它們在建立內容片段時可供作者使用。
* 刪除 — 始終需要刪除，但您需要注意刪除已用於內容片段的模型，特別是已發佈的片段。

## 發佈 {#publishing}

<!-- needs more details -->

在發佈任何相關內容片段時/之前，需要發佈內容片段模型。

>[!NOTE]
>
>如果作者嘗試發佈模型尚未發佈的內容片段，則選擇清單將指示此情況，並且模型將隨該片段一起發佈。

一旦模型發佈， *鎖定* 在作者上進入只讀模式。 這旨在防止導致現有GraphQL架構和查詢出錯的更改，特別是在發佈環境中。 在控制台中，它由 **鎖定**。

當模型為 **鎖定** （在只讀模式下），可以看到模型的內容和結構，但不能直接編輯；儘管你可以 **鎖定** 控制台或模型編輯器中的模型。

## 下一步 {#whats-next}

現在您已經掌握了基本知識，下一步就是開始建立您自己的內容片段模型。

## 其他資源 {#additional-resources}

* [製作概念](/help/sites-cloud/authoring/getting-started/concepts.md)

* [基本處理](/help/sites-cloud/authoring/getting-started/basic-handling.md)  — 本頁主要基於 **站點** 控制台，但許多/大多數功能也與導航和對其執行操作相關， **內容片段模型** 下 **常規** 控制台。

* [使用內容片段](/help/assets/content-fragments/content-fragments.md)

   * [內容片段模型](/help/assets/content-fragments/content-fragments-models.md)

      * [定義內容片段模型](/help/assets/content-fragments/content-fragments-models.md#defining-your-content-fragment-model)

      * [啟用或禁用內容片段模型](/help/assets/content-fragments/content-fragments-models.md#enabling-disabling-a-content-fragment-model)

      * [允許在資產資料夾上建立內容片段模型](/help/assets/content-fragments/content-fragments-models.md#allowing-content-fragment-models-assets-folder)

      * [刪除內容片段模型](/help/assets/content-fragments/content-fragments-models.md#deleting-a-content-fragment-model)

      * [發佈內容片段模型](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model)

      * [取消發佈內容片段模型](/help/assets/content-fragments/content-fragments-models.md#unpublishing-a-content-fragment-model)

      * [鎖定（已發佈）內容片段模型](/help/assets/content-fragments/content-fragments-models.md#locked-published-content-fragment-models)

* 入門指南

   * [建立內容片段模型無頭設定](/help/headless/setup/create-content-model.md)
