---
title: 如何傳送最適化表單以供檢閱？
description: 共用最適化表單以供一或多個稽核者稽核。
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
source-git-commit: 57e421a865b664c0adb7af93b33bd4b6b32049ab
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---


# 將提交稽核者與表單建立關聯 {#associating-submission-reviewers-with-a-form}

建立表單時，您可以指定透過表單入口網站稽核表單提交內容並提供意見回饋的使用者。 您的組織可以收集意見並對提交的表單進行重新處理。

[!DNL AEM Forms] 可讓您將稽核者群組與表單建立關聯。 新增至表單稽核群組的使用者可以檢視此表單的提交內容，並提供意見反應。

指派給表單的稽核者群組只能稽核指定表單的提交。

## 必備條件 {#prerequisite}

### 使用中繼資料結構編輯器啟用最適化Forms的提交檢閱者群組屬性 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

若要將檢閱者群組與表單建立關聯，請編輯Adaptive Forms的中繼資料結構。 依預設，您無法將稽核者群組新增至提交的表單。

若要編輯中繼資料結構：

1. 在作者模式中的Experience Manager下方，按一下 **工具** > **資產** > **中繼資料結構**.
1. 在「結構Forms」頁面中，導覽至 **Forms** > **Forms在AEM中編寫。**

   頁面的URL為：

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 選取 **最適化表單** 並按一下 **編輯**.
1. 在「編輯表單」頁面中，按一下 **進階**.
1. 在「進階」標籤中，拖放 **單行文字** 「建置表單」下可用的元件。
1. 選取新增的文字元件以檢視其設定。

   在設定下，輸入 `./jcr:content/metadata/form-submission-reviewer-group` （在對應至屬性欄位中）。

   您的最適化表單的「進階」屬性中的提交稽核者群組欄位會以您在「欄位標籤」下指定的名稱啟用。

## 將提交稽核者與表單建立關聯 {#associating-submission-reviewers-with-a-form-1}

若要將提交稽核者與最適化表單建立關聯，請建立稽核者群組並將使用者新增至該群組。 在表單的進階屬性中，於表單提交稽核者欄位下新增建立的稽核者群組。
使用者群組可讓您將不同的提交稽核者集與不同的Adaptive Forms建立關聯。 此功能可防止未經授權的使用者進行提交稽核。

執行以下步驟之前，請參閱 [先決條件](adding-reviewers-form.md#prerequisite).

若要建立群組並新增成員，請瀏覽至 **工具** > **作業** > **安全性** > **群組**.
如需詳細資訊，請參閱 [使用者管理與服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html).
確定您將建立的群組新增為現成可用的使用者群組的成員： **表單 — 提交 — 稽核者**. 此使用者群組隨附於 [!DNL AEM Forms]，並確保將使用者新增為提交稽核者。

若要將使用者群組與最適化表單產生關聯：

1. 在撰寫模式中，導覽至 **Forms** > **Forms與檔案**.
1. 使用**選取**選項選取最適化表單，然後按一下 **檢視屬性**.
1. 在表單的「屬性」視窗中，按一下 **編輯**，然後按一下 **進階**.
1. 在提交稽核者群組欄位中輸入群組，然後按一下 **完成**.

   提交稽核者群組欄位會以您在Adaptive Forms的已編輯中繼資料結構中所指定的名稱顯示。

>[!NOTE]
>
>複製使用者和表單，以確保使用者與表單在遠端實作中的可用性 [!DNL AEM Forms].
>
>確定所有使用者都復寫為檢閱遠端實作中使用者群組的成員。

>[!MORELIKETHIS]
>
>* [建立和管理表單的稽核](/help/forms/create-reviews-forms.md)
>* [建立和管理最適化表單的稽核](/help/forms/review-adaptiveforms-in-sites-page.md)