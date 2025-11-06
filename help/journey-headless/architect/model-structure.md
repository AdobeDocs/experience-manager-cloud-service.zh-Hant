---
title: 了解如何在 AEM 中建立內容片段模型
description: 了解使用內容片段模型建立 Headless CMS 內容模型的概念和機制。
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 83%

---

# 了解如何在 AEM 中建立內容片段模型 {#architect-headless-content-fragment-models}

## 目前進度 {#story-so-far}

在[AEM Headless 內容作者歷程](overview.md)的一開始，[AEM Headless 內容模型基本知識](basics.md)介紹了和 Headless 內容製作相關的基本概念和術語。

此文章以這些原則為基礎，讓您了解如何為 AEM Headless 專案建立自己的內容片段模型。

## 目標 {#objective}

* **客群**：初學者
* **目標**：使用內容片段模型為您的 Headless CMS 建立內容模型的概念和機制。

## 建立內容片段模型 {#creating-content-fragment-models}

然後可以建立內容片段模型並定義其結構。

1. 在內容片段主控台中，選擇內容片段模型面板。

1. 根據您的設定或子設定導覽至適合的資料夾。

1. 使用「**建立**」開啟「**新內容片段模型**」對話框。

   ![標題和說明](/help/sites-cloud/administering/content-fragments/assets/cf-managing-content-fragment-models-create.png)

1. 填寫詳細資訊

1. 使用「**建立**」來儲存空模型，或選擇「**建立並開啟**」。

## 定義內容片段模型 {#defining-content-fragment-models}

第一次開啟新模型時，您會看到 — 中間有一個大的（相當大的）空白區域，左側有&#x200B;**個資料型別**&#x200B;的長清單，右側有&#x200B;**個屬性** （一開始是空的，就像所選欄位一樣）：

![空白模型](/help/sites-cloud/administering/content-fragments/assets/cf-cfmodels-empty-model.png)

那麼 -該怎麼做？

下列兩個動作您可以擇一執行：

* 將資料型別從左側面板拖曳至中間面板中欄位的必要位置。
* 依資料型別選取+圖示以將其新增至欄位清單底部。
* 選取中間面板中的「新增」 ，然後從產生的下拉式清單中選取所需的資料型別，以在清單底部新增欄位。

您已在定義模型！

新增資料類型後，您需要為該欄位定義&#x200B;**屬性**。所使用的類型會決定這些屬性。例如：

![資料屬性](/help/sites-cloud/administering/content-fragments/assets/cf-cfmodels-field-properties.png)

### 您的內容作者 {#your-content-authors}

您的內容作者看不到您用於建立模型的實際資料類型和屬性。這表示您可能必須提供相關協助和資訊讓他們完成特定欄位。對於基本資訊，您可以使用欄位標籤和預設值，但可能需要考慮更複雜案例的專案特定文件。

>[!NOTE]
>
>請參閱其他資源 - 內容片段模型。

## 管理內容片段模型 {#managing-content-fragment-models}

<!-- needs more details -->

管理您的內容片段模型涉及：

* 啟用 (或停用) 它們 - 這使作者在建立內容片段時可以使用。
* 刪除 - 總是需要刪除功能，但您必須注意不要刪除已經有內容片段在使用的模型，特別是已發佈的片段。

## 發佈 {#publishing}

<!-- needs more details -->

內容片段模型需要在任何相關內容片段發佈時/之前發佈。

>[!NOTE]
>
>如果作者想要發佈的內容片段尚未發佈其模型，在這個情況下會出現選取清單，而模型會與片段一起發佈。

一旦模型發佈，就會被&#x200B;*鎖定*&#x200B;成作者的唯讀模式。這旨在防止可能導致現有 GraphQL 結構和查詢錯誤的變更，尤其是在發佈環境。它在主控台中顯示為&#x200B;**鎖定**。

當模型為&#x200B;**鎖定** (唯讀模式) 時，可以看到模型的內容和結構，但不能直接編輯；儘管您可以從主控台或模型編輯器管理&#x200B;**鎖定**&#x200B;模型。

## 後續步驟 {#whats-next}

現在您已經了解了基本知識，下一步是開始建立您自己的內容片段模型。

## 其他資源 {#additional-resources}

* [製作概念](/help/sites-cloud/authoring/author-publish.md)

* [基本處理](/help/sites-cloud/authoring/basic-handling.md) - 此頁面主要基於 **Sites** 主控台，但許多/大多數功能也與導覽至&#x200B;**一般**&#x200B;主控台下&#x200B;**內容片段模型**&#x200B;及對其採取行動相關。

* [使用內容片段](/help/sites-cloud/administering/content-fragments/overview.md)

   * [內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [定義內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

      * [啟用或停用內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#enabling-disabling-a-content-fragment-model)

      * [允許資產資料夾中的內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder)

      * [刪除內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#deleting-a-content-fragment-model)

      * [發佈內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model)

      * [取消發佈內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#unpublishing-a-content-fragment-model)

      * [鎖定的內容片段模型](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#locked-content-fragment-models)

* 快速入門指南

   * [建立內容片段模型 - Headless 設定](/help/headless/setup/create-content-model.md)
