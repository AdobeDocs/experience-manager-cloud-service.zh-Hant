---
title: 如何將核心元件型最適化表單儲存為草稿，並使用草稿和提交元件來列出草稿和提交？
description: 瞭解如何將基於核心元件的最適化表單另存為草稿。 也瞭解如何使用草稿和提交元件來列出登入使用者的草稿和提交？
feature: Adaptive Forms, Core Components
exl-id: c0653bef-afeb-40c1-b131-7d87ca5542bc
role: User, Developer
source-git-commit: 8f1fa3a95f232f34ad6ae89c391e9e2272a2c072
workflow-type: tm+mt
source-wordcount: '1385'
ht-degree: 3%

---


# 將表單另存為草稿並列在網站頁面上

<!--This article provides information about the Auto-save feature, which is currently available as a pre-release feature. The pre-release feature is accessible only through our [pre-release channel](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/release-notes/prerelease#new-features).-->

假設使用者開始填寫表單，但需要暫停並在稍後返回。 AEM提供`save-as-draft`選項，讓使用者可將表單儲存為草稿以供日後完成。 為方便起見，AEM提供現成的&#x200B;**草稿與提交** Forms Portal元件，可在AEM Sites頁面上顯示草稿與提交。 元件會列出已儲存為草稿以供稍後完成的表單，以及已提交的表單。 只有登入的使用者可以編輯其草稿或檢視其提交的表單。 但是，如果匿名使用者使用&#x200B;**搜尋與清單製作者**&#x200B;元件瀏覽表單清單，並將表單儲存為草稿，則&#x200B;**草稿與提交**&#x200B;元件不會列出該草稿。 若要檢視草稿和提交，使用者必須在提交表單時登入。

![草稿圖示](assets/drafts-component.png)

## 必要條件

* 安裝最新的Far，為AEM Cloud Service環境啟用最適化Forms核心元件。

  將最新核心元件部署至您的環境後，您便可在編寫環境中存取Forms Portal元件。

* [為草稿和提交設定Azure儲存體和統一儲存體聯結器Forms入口網站元件](#configure-azure-storage-and-unified-storage-connector-for-drafts--submissions-forms-portal-component)

### 為草稿和提交設定Azure儲存和統一儲存聯結器Forms入口網站元件

**草稿和提交**&#x200B;元件需要儲存設定，才能在AEM Sites頁面上儲存和列出草稿。 統一儲存聯結器提供將AEM與外部儲存裝置連結的架構。 若要將表單儲存為草稿，請確定您擁有Azure儲存體帳戶和存取金鑰，以授權存取[!DNL Azure]儲存體帳戶。 擁有Azure儲存體帳戶和存取金鑰後，請執行以下步驟來建立Azure儲存體設定：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL 雲端服務]** > **[!UICONTROL Azure儲存空間]**。

   ![選擇Azure儲存卡](/help/forms/assets/save-form-as-draft-azure-card.png)

1. 選取設定資料夾以建立設定，並選取&#x200B;**[!UICONTROL 建立]**。

   ![選取Azure儲存設定資料夾](/help/forms/assets/save-form-as-draft-select-config-folder.png)

1. 在&#x200B;**[!UICONTROL 標題]**&#x200B;欄位中指定組態的標題。
1. 在[!DNL Azure]Azure儲存體帳戶&#x200B;**[!UICONTROL 和]** Azure存取金鑰&#x200B;**[!UICONTROL 欄位中指定]**&#x200B;儲存體帳戶的名稱。

   ![Azure 儲存體設定](/help/forms/assets/save-form-as-draft-azure-storage.png)

   在`Connection String`文字方塊中輸入`Azure Storage Account`，在`Azure Key`文字方塊中輸入`Azure Access key`。

1. 按一下&#x200B;**儲存**。

   >[!NOTE]
   >
   > 您可以從&#x200B;**[!UICONTROL Microsoft Azure入口網站]**&#x200B;擷取&#x200B;**[!UICONTROL Azure儲存體帳戶]**&#x200B;和[Azure存取金鑰](https://learn.microsoft.com/en-us/azure/storage/common/storage-account-keys-manage?tabs=azure-portal)。

   成功建立Azure儲存體設定後，請使用下列步驟設定Forms Portal的統一儲存體聯結器：

1. 導覽至&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Forms]** > **[!UICONTROL 整合式儲存聯結器]**。

   ![統一的聯結器存放區](/help/forms/assets/save-form-as-draft-unified-connector.png)

1. 在&#x200B;**[!UICONTROL Forms入口網站]**&#x200B;區段中，從&#x200B;**[!UICONTROL 儲存體]**&#x200B;下拉式清單中選取&#x200B;**[!UICONTROL Azure]**。
1. 在&#x200B;**[!UICONTROL 儲存設定路徑]**&#x200B;欄位中指定Azure儲存體設定的設定路徑。

   ![統一的聯結器儲存設定](/help/forms/assets/save-form-as-draft-unified-connector-storage.png)

1. 選取「**[!UICONTROL 儲存]**」。

>[!NOTE]
>
> 如果您需要設定Azure以外的儲存選項，請從您的正式電子郵件地址寄信至aem-forms-ea@adobe.com並提供您詳細的需求。

當您成功設定Azure儲存體和統一儲存體聯結器以儲存草稿和已提交的表單後，請在AEM Sites頁面上新增&#x200B;**草稿和提交**&#x200B;元件。

## 如何將草稿和提交元件新增到AEM Sites頁面？

您可以使用現成可用的Forms Portal元件，在Sites頁面上列出草稿和提交內容。 執行以下步驟以新增&#x200B;**草稿和提交**&#x200B;入口網站元件：

1. 以&#x200B;**編輯**&#x200B;模式開啟AEM Sites頁面。
1. 移至&#x200B;**[!UICONTROL 頁面資訊]** > **[!UICONTROL 編輯範本]**
   ![編輯範本原則](/help/forms/assets/save-form-as-draft-edit-template.png)

1. 按一下&#x200B;**[!UICONTROL 原則]**，然後選取&#x200B;**[!UICONTROL AEM原型專案名稱]** - Forms和通訊入口網站&#x200B;**[下的]草稿與提交**&#x200B;核取方塊。

   ![原則選擇](/help/forms/assets/save-form-as-draft-enable-policy.png)

1. 按一下&#x200B;**[!UICONTROL 完成]**。
1. 現在，請在撰寫模式中重新開啟AEM Sites頁面。
1. 在頁面編輯器中找出區段，讓您新增Forms Portal元件。
1. 按一下&#x200B;**新增**&#x200B;圖示。 圖示是加號(+)，表示可新增元件的選項。

   按一下&#x200B;**新增**&#x200B;圖示會顯示&#x200B;**插入新元件**&#x200B;對話方塊，其中顯示要插入的各種元件。

   >[!NOTE]
   >
   > 或者，您也可以拖放元件。

1. 瀏覽對話方塊中的可用元件，並從清單中選取所需元件。 例如，從清單中選取&#x200B;**草稿和提交**&#x200B;元件，以新增&#x200B;**草稿和提交** Forms入口網站元件。

   ![新增草稿與提交元件](/help/forms/assets/save-form-as-draft-add-dns.png)

現在，根據需求設定&#x200B;**草稿和提交**&#x200B;元件的屬性。

## 設定草稿和提交元件的屬性

您可以設定&#x200B;**草稿與提交**&#x200B;的屬性：
1. 選取&#x200B;**草稿與提交**&#x200B;元件。
1. 按一下![設定圖示](assets/configure_icon.png)，對話方塊就會顯示。
1. 在&#x200B;**[!UICONTROL 草稿和提交]**&#x200B;對話方塊中，指定下列專案：
   * **標題**&#x200B;若要識別Sites頁面中的元件，根據預設，標題會顯示在元件上方。
   * **選取型別**：表示表單清單為草稿或已提交的表單。 如果您選擇&#x200B;**草稿Forms**，則會顯示儲存為草稿的表單。 或者，選取&#x200B;**已提交的Forms**&#x200B;會顯示由登入使用者提交的表單。
   * **配置**：以卡片或清單格式顯示清單草稿表單或已提交的表單。

   ![草稿與提交元件屬性](/help/forms/assets/save-form-as-draft-dns-properties.png)

## 設定表單以另存為草稿

您可以透過以下兩種方式設定最適化Forms，以儲存為草稿供日後使用：
* [使用者動作](#user-action)
* [自動儲存](#auto-save)

### 使用者動作

>[!NOTE]
>
> 請確定[核心元件版本設定為3.0.24或更新版本](https://github.com/adobe/aem-core-forms-components)，以使用&#x200B;**儲存表單**&#x200B;規則將表單儲存為草稿。

若要將表單儲存為草稿，請在表單元件（例如按鈕）上建立&#x200B;**儲存表單**&#x200B;規則。 按一下按鈕時會觸發規則，而表單會儲存為草稿。 執行以下步驟，在按鈕元件上建立&#x200B;**儲存表單**&#x200B;規則：

1. 以編輯模式開啟最適化表單。
1. 選取&#x200B;**[!UICONTROL 編輯規則]**&#x200B;圖示以開啟&#x200B;**按鈕**&#x200B;元件的規則編輯器。
1. 選取&#x200B;**[!UICONTROL 建立]**&#x200B;以設定和建立按鈕的規則。
1. 在&#x200B;**[!UICONTROL When]**&#x200B;區段中，選取&#x200B;**已點按**，並在&#x200B;**[!UICONTROL Then]**&#x200B;區段中，選取&#x200B;**儲存表單**&#x200B;選項。
1. 選取「**[!UICONTROL 完成]**」以儲存此規則。

   ![建立按鈕](/help/forms/assets/save-form-as-drfat-create-rule.png)的規則

當您預覽最適化表單並填寫時，按一下&#x200B;**儲存表單**&#x200B;按鈕，表單會儲存為草稿。

### 草稿

>[!NOTE]
>
> 請確定[核心元件版本設為3.0.52或更新版本](https://github.com/adobe/aem-core-forms-components)，以使用自動儲存功能將表單儲存為草稿。

您也可以設定最適化表單，以根據時間型事件自動儲存，確保表單在指定期間後儲存。 當您[為您的環境](/help/forms/list-forms-on-sites-page.md#enable-forms-portal-components-for-your-existing-environment)啟用Forms Portal元件時，**自動儲存**&#x200B;索引標籤會出現在Forms容器屬性中。 您可以為最適化表單設定自動儲存功能：

1. 在作者執行個體中，以編輯模式開啟調適型表單。
1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下節目表容器屬性![節目表屬性](/help/forms/assets/configure-icon.svg)圖示，然後開啟&#x200B;**[!UICONTROL 草稿]**&#x200B;標籤。

   ![自動儲存](/help/forms/assets/auto-save.png)

1. 選取&#x200B;**[!UICONTROL 自動儲存草稿]**&#x200B;核取方塊，以啟用將表單自動儲存為草稿。
1. 將&#x200B;**[!UICONTROL 儲存喜好設定]**&#x200B;設定為&#x200B;**定期儲存草稿**，以在特定時間間隔後自動儲存表單<!--based on the occurrence of an event or-->。
1. 以&#x200B;**[!UICONTROL 儲存間隔頻率（秒）]**&#x200B;指定時間間隔，以設定在定義的間隔觸發自動儲存表單的持續時間。
1. 按一下&#x200B;**[!UICONTROL 完成]**。

## 使用草稿和提交元件在「網站」頁面上檢視草稿/提交的表單

若要檢視已儲存的草稿或已提交的表單，請使用&#x200B;**草稿與提交** Forms入口網站元件。
在「草稿與提交」元件**[!UICONTROL 的]**&#x200B;設定對話方塊中，選取&#x200B;**選取型別**&#x200B;作為[草稿Forms](#configure-properties-of-the-drafts--submissions-component)時，儲存為草稿的表單會顯示在「網站」頁面上。 您可以按一下省略符號(...)來開啟草稿以完成表單。

![草稿圖示](assets/drafts-component.png)

在「草稿與提交」元件&#x200B;**[!UICONTROL 的]**&#x200B;設定對話方塊中，當&#x200B;**選取型別**&#x200B;選取為[已提交的Forms](#configure-properties-of-the-drafts--submissions-component)時，已提交的表單就會出現。 您可以檢視已提交的表單，但無法編輯它們。

![提交圖示](assets/submission-listing.png)

您也可以按一下表單右下角出現的省略符號(...)來捨棄表單。

>[!NOTE]
>
> Forms入口網站中的提交專案清單只會顯示Foundation表單提交專案。

## 後續步驟

在下一篇文章中，讓我們瞭解[如何使用連結Forms入口網站元件](/help/forms/add-form-link-to-aem-sites-page.md)，在網站頁面上新增表單參考。

## 相關的文章

{{forms-portal-see-also}}

## 另請參閱 {#see-also}

{{see-also}}