---
title: 在Forms Manager中管理表單版本
description: 瞭解如何在Forms Manager UI中建立和管理最適化Forms、表單片段、主題和其他資產的版本。
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="適用於AEM Forms)。"
exl-id: cd2c6e15-99a6-4b4e-bfd1-8291a2001ebe
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 5%

---

# 在Forms Manager UI中管理表單Assets版本

<span class="preview">此功能可透過搶先存取計畫使用。 若要要求存取權，請從您的正式地址傳送電子郵件至[aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)。</span>

Forms Manager現在支援表單資產的版本設定。 您可以從Forms Manager UI建立資產的版本、檢視版本歷程記錄和還原舊版。

## 支援的資產型別 {#supported-asset-types}

您可以建立和管理以下資產型別的版本：

| 資產類型 | 說明 |
|---|---|
| 最適化Forms （核心元件） | 使用核心元件建立的最適化Forms |
| 最適化Forms （基礎元件） | 使用基礎元件建置的最適化Forms |
| 表單片段 | 可重複使用的表單區段可跨多個表單共用 |
| 主題 | 套用至最適化Forms的視覺樣式定義 |
| XDP範本 | 以XFA為基礎的表單範本 |
| 二進位資產 | 儲存在表單DAM存放庫下的其他檔案 |

## 建立版本 {#create-version-forms-manager}

若要建立表單資產的版本：

1. 導覽至「**[!UICONTROL Adobe Experience Manager]**」>「**[!UICONTROL 「表單]**」>「**[!UICONTROL 表單與文件]**」。
1. 選取表單或資產。
1. 在左側面板中，選取&#x200B;**[!UICONTROL 時間表]**。
1. 按一下時間軸工具列中的&#x200B;**[!UICONTROL 另存為版本]**。
   ![另存為版本](/help/forms/assets/create-version.png)
1. 輸入&#x200B;**[!UICONTROL 標籤]**&#x200B;和選用的&#x200B;**[!UICONTROL 註解]**&#x200B;來說明變更。
1. 按一下「**[!UICONTROL 建立]**」。
   ![另存為版本2](/help/forms/assets/create-version1.png)

版本會以其標籤、註解及時間戳記出現在時間軸面板中。

## 上傳時版本化資產 {#version-on-upload}

當您上傳與現有資產同名的資產時，Forms Manager會顯示&#x200B;**檔案上傳**&#x200B;對話方塊，其中列出要更新的資產。 該對話方塊會顯示資產名稱、區段和路徑。

當具有相同名稱的資產已存在時，上傳會自動替換現有資產並建立新版本。 您可以在時間軸中檢視建立的版本。

![檔案上傳對話方塊顯示已建立版本的上傳](/help/forms/assets/version-upload.png)

## 檢視版本記錄 {#view-version-history}

若要檢視資產的版本記錄：

1. 在Forms Manager中選取資產。
1. 在左側面板中，選取&#x200B;**[!UICONTROL 時間表]**。
   ![版本記錄](/help/forms/assets/version-history.png)

時間軸會顯示所有版本專案以及活動事件。 每個專案都會顯示標籤、註解、作者及時間戳記。

## 還原先前版本 {#restore-version}

若要將資產還原為舊版：

1. 在Forms Manager中選取資產。
1. 在左側面板中，選取&#x200B;**[!UICONTROL 時間表]**。
1. 選取您要還原的版本。
1. 按一下&#x200B;**[!UICONTROL 還原為此版本]**。
   ![還原版本](/help/forms/assets/revert-version.png)

>[!NOTE]
>
>影像無法還原成先前的版本。 所有其他資產型別(包括Adaptive Forms、表單片段、主題和XDP範本)都支援版本還原。

## 另請參閱 {#see-also}

* [最適化表單的版本設定、稽核和註解](/help/forms/add-comments-annotations-versioning-adaptive-form-core-components.md)
* [匯入和匯出表單和相關資產](/help/forms/import-export-forms-templates.md)
* [發佈和取消發佈表單](/help/forms/publishing-unpublishing-forms.md)
