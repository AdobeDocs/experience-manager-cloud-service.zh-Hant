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
source-wordcount: '493'
ht-degree: 0%

---


# 將提交稽核者與表單建立關聯 {#associating-submission-reviewers-with-a-form}

建立表單時，您可以指定透過表單入口網站稽核表單提交內容並提供意見回饋的使用者。 您的組織可以收集意見並對提交的表單進行重新處理。

[!DNL AEM Forms]可讓您將檢閱者群組與表單建立關聯。 新增至表單稽核群組的使用者可以檢視此表單的提交內容，並提供意見反應。

指派給表單的稽核者群組只能稽核指定表單的提交。

## 必備條件 {#prerequisite}

### 使用中繼資料結構編輯器啟用最適化Forms的提交檢閱者群組屬性 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

若要將檢閱者群組與表單建立關聯，請編輯Adaptive Forms的中繼資料結構。 依預設，您無法將稽核者群組新增至提交的表單。

若要編輯中繼資料結構：

1. 在作者模式的Experience Manager底下，按一下&#x200B;**工具** > **Assets** > **中繼資料結構描述**。
1. 在「結構描述Forms」頁面中，導覽至&#x200B;**Forms** > **在AEM中撰寫的Forms。**

   頁面的URL為：

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 選取&#x200B;**最適化表單**&#x200B;並按一下&#x200B;**編輯**。
1. 在[編輯表單]頁面中，按一下[**進階**]。
1. 在[進階]索引標籤中，拖放[建置表單]下可用的&#x200B;**單行文字**&#x200B;元件。
1. 選取新增的文字元件以檢視其設定。

   在[設定]下，在[對應至屬性]欄位中輸入`./jcr:content/metadata/form-submission-reviewer-group`。

   您的最適化表單的「進階」屬性中的提交稽核者群組欄位會以您在「欄位標籤」下指定的名稱啟用。

## 將提交稽核者與表單建立關聯 {#associating-submission-reviewers-with-a-form-1}

若要將提交稽核者與最適化表單建立關聯，請建立稽核者群組並將使用者新增至該群組。 在表單的進階屬性中，於表單提交稽核者欄位下新增建立的稽核者群組。
使用者群組可讓您將不同的提交稽核者集與不同的Adaptive Forms建立關聯。 此功能可防止未經授權的使用者進行提交稽核。

執行以下步驟之前，請參閱[先決條件](adding-reviewers-form.md#prerequisite)。

若要建立群組並新增成員，請瀏覽至&#x200B;**工具** > **作業** > **安全性** > **群組**。
如需詳細資訊，請參閱[使用者管理與服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html)。
請確定您將建立的群組新增為現成使用者群組的成員： **forms-submission-reviewers**。 此使用者群組已隨附[!DNL AEM Forms]，而且可確保將使用者新增為提交稽核者。

若要將使用者群組與最適化表單產生關聯：

1. 在撰寫模式中，導覽至&#x200B;**Forms** > **Forms和檔案**。
1. 使用**選取**選項選取最適化表單，然後按一下&#x200B;**檢視屬性**。
1. 在表單的[內容]視窗中，按一下[**編輯**]，然後按一下[**進階**]。
1. 在提交稽核者群組欄位中輸入群組，然後按一下&#x200B;**完成**。

   提交稽核者群組欄位會以您在Adaptive Forms的已編輯中繼資料結構中所指定的名稱顯示。

>[!NOTE]
>
>復寫使用者和表單，以確保[!DNL AEM Forms]的遠端實作中使用者和表單的可用性。
>
>確定所有使用者都復寫為檢閱遠端實作中使用者群組的成員。

>[!MORELIKETHIS]
>
>* [建立和管理表單的稽核](/help/forms/create-reviews-forms.md)
>* [建立和管理最適化表單的稽核](/help/forms/review-adaptiveforms-in-sites-page.md)