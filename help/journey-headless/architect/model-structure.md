---
title: 了解如何在 AEM 中建立內容片段模型
description: 了解使用內容片段模型建立 Headless CMS 內容模型的概念和機制。
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 6306ad88b889197aff377dc0a72ea232cd76ff9c
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 76%

---

# 了解如何在 AEM 中建立內容片段模型 {#architect-headless-content-fragment-models}

## 目前進度 {#story-so-far}

在[AEM Headless 內容作者歷程](overview.md)的一開始，[AEM Headless 內容模型基本知識](basics.md)介紹了和 Headless 內容製作相關的基本概念和術語。

本文基於這些原則，好讓您瞭解如何為您的AEM Headless專案建立自己的內容片段模型。

## 目標 {#objective}

* **客群**：初學者
* **目標**：使用內容片段模型為您的 Headless CMS 建立內容模型的概念和機制。

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools > General > Configuration Browser. You can either select to configure the global entry, or create a configuration. For example:

![Define configuration](/help/sites-cloud/administering/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## 建立內容片段模型 {#creating-content-fragment-models}

接著，即可建立內容片段模型並定義結構。

1. 在內容片段主控台中，選取內容片段模式的面板。

1. 導覽至適合您組態或子組態的資料夾。

1. 使用&#x200B;**建立**&#x200B;開啟&#x200B;**新內容片段模式**&#x200B;對話方塊。

   ![標題和說明](/help/sites-cloud/administering/content-fragments/assets/cf-managing-content-fragment-models-create.png)

1. 完成詳細資料

1. 使用&#x200B;**建立**&#x200B;儲存空的模型，或使用&#x200B;**建立並開啟**。

<!--
Then the Content Fragments Models can be created and the structure defined. This can be done under **Tools** > **General** > **Content Fragment Models**. 

![Content Fragment Models in Tools](assets/cfm-tools.png)

After selecting this you navigate to the location for your model and select **Create**. Here you can enter various key details.

The option **Enable model** is activated by default. This means that your model is available for use (in creating Content Fragments) as soon as you have saved it. You can deactivate this if you want - there are opportunities later to enable (or disable) an existing model.

![Create Content Fragment Model](/help/sites-cloud/administering/content-fragments/assets/cfm-models-02.png)

Confirm with **Create** and you can then **Open** your model to start defining the structure.
-->

## 定義內容片段模型 {#defining-content-fragment-models}

當您首次開啟新模型時，您會看到左側有一大片空白，右側有一長串「**資料類型**」：

![空白模型](/help/sites-cloud/administering/content-fragments/assets/cfm-models-03.png)

那麼 -該怎麼做？

您可以將&#x200B;**資料類型**&#x200B;的執行個體拖曳到左側空間 - 您已經定義了模型！

![定義欄位](/help/sites-cloud/administering/content-fragments/assets/cfm-models-04.png)

新增資料類型後，您需要為該欄位定義&#x200B;**屬性**。這些屬性取決於所使用的型別。 例如：

![資料屬性](/help/sites-cloud/administering/content-fragments/assets/cfm-models-05.png)

您可以隨您所需新增多個欄位。例如：

![內容片段模型](/help/sites-cloud/administering/content-fragments/assets/cfm-models-07.png)

### 您的內容作者 {#your-content-authors}

您的內容作者看不到您用於建立模型的實際資料類型和屬性。這表示您可能必須提供相關協助和資訊讓他們完成特定欄位。對於基本資訊，您可以使用欄位標籤和預設值，但可能需要考慮更複雜案例的專案特定文件。

>[!NOTE]
>
>請參閱其他資源 - 內容片段模型。

## 管理內容片段模型 {#managing-content-fragment-models}

<!-- needs more details -->

管理您的內容片段模型涉及：

* 啟用 (或停用) 它們 - 這使作者在建立內容片段時可以使用。
* 刪除 — 一律需要刪除，但您需要注意刪除已用於內容片段的模型；尤其是已發佈的片段。

## 發佈 {#publishing}

<!-- needs more details -->

內容片段模型需要在任何相關內容片段發佈時/之前發佈。

>[!NOTE]
>
>如果作者嘗試發佈尚未發佈模型的內容片段，選擇清單會指出這一點，並且模型會與片段一起發佈。

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
