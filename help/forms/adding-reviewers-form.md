---
title: 將提交審核者與表單關聯
seo-title: Associating submission reviewers with a form
description: 瞭解如何將提交審核者與表單關聯 [!DNL AEM Forms]。 關聯的審閱者審閱通過表單門戶提交的表單。
seo-description: Learn how to associate submission reviewers with a form in [!DNL AEM Forms]. Associated reviewers review a form submitted via forms portal.
uuid: 58c8c8fb-9262-4c37-b9b2-e46fe21b77d9
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 71d1aa10-d191-49bc-a50f-1098324f1cfe
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---


# 將提交審核者與表單關聯 {#associating-submission-reviewers-with-a-form}

建立表單時，您可以指定通過表單門戶查看表單提交並提供反饋的用戶。 您的組織可以收集對已提交表單的反饋和返工。

[!DNL AEM Forms] 允許您將審閱者組與表單關聯。 添加到表單的審閱組的用戶可以查看此表單的提交並提供反饋。

分配給表單的審閱者組只能審閱指定表單的提交。

## 必備條件 {#prerequisite}

### 使用元資料架構編輯器為Adaptive Forms啟用提交審閱者組屬性 {#enabling-submission-reviewer-groups-property-for-adaptive-forms-using-metadata-schema-editor}

要將審閱者組與表單關聯，請編輯AdaptiveForms的元資料架構。 預設情況下，無法將審閱者組添加到已提交的表單中。

要編輯元資料架構：

1. 在作者模式下，在Experience Manager下，按一下 **工具** > **資產** > **元資料架構**。
1. 在「架構Forms」頁中，導航到 **Forms** > **FormsAEM。**

   該頁的URL為：

   ```html
   https://<hostname>:<port>/mnt/overlay/dam/gui/content/metadataschemaeditor/
    schemalist.html/forms/aem-authored
   ```

1. 選擇 **自適應窗體** 按一下 **編輯**。
1. 在「編輯表單」頁中，按一下 **高級**。
1. 在「高級」頁籤中，拖放 **單行文本** 元件在「生成表單」下可用。
1. 選擇添加的文本元件以查看其設定。

   在設定下，輸入 `./jcr:content/metadata/form-submission-reviewer-group` 在「映射到屬性」欄位中。

   使用在「欄位標籤」下指定的名稱啟用「自適應表單的高級屬性」中的提交審閱者組欄位。

## 將提交審核者與表單關聯 {#associating-submission-reviewers-with-a-form-1}

要將提交審閱者與自適應表單關聯，請建立審閱者組並向其添加用戶。 在表單的高級屬性中的表單提交審閱者欄位下添加建立的審閱者組。
用戶組允許您將不同的提交審核者集與不同的自適應Forms關聯。 此功能可防止未經授權的用戶進行提交審閱。

在執行以下步驟之前，請參見 [先決條件](adding-reviewers-form.md#prerequisite)。

要建立組並向其添加成員，請導航至 **工具** > **操作** > **安全** > **組**。
有關詳細資訊，請參見 [用戶管理和服務](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security.html)。
確保添加作為出廠設定用戶組成員建立的組： **表單提交審核者**。 此用戶組隨附 [!DNL AEM Forms]，並確保將用戶添加為提交審閱者。

要將用戶組與自適應表單關聯：

1. 在創作模式中，導航到 **Forms** > **Forms和文檔**。
1. 使用**選擇**選項選擇自適應表單，然後按一下 **查看屬性**。
1. 在窗體的「屬性」窗口中，按一下 **編輯**，然後按一下 **高級**。
1. 在提交審閱者組欄位中輸入組，然後按一下 **完成**。

   此時將顯示提交審閱者組欄位，其名稱在已編輯的AdaptiveForms元資料架構中指定。

>[!NOTE]
>
>複製用戶和表單以確保在遠程實施中用戶和表單的可用性 [!DNL AEM Forms]。
>
>確保將所有用戶複製為遠程實施中查看用戶組成員。

