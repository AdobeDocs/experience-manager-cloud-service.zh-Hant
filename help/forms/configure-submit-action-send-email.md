---
Title: How to send an email on submission of an Adaptive Form?
Description: Explore the process to set up email notifications when submitting an Adaptive Form.
keywords: 如何傳送最適化表單的電子郵件、電子郵件提交動作、最適化表單電子郵件、表單提交電子郵件、傳送電子郵件指南
feature: Adaptive Forms, Core Components, Foundation Components, Edge Delivery Services
exl-id: 70386e57-345b-4edb-97f1-3fd52ea9ff4f
title: 如何設定最適化表單的提交動作？
role: User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 19%

---

# 設定最適化表單的傳送電子郵件提交動作

**[!UICONTROL 傳送電子郵件]**&#x200B;提交動作可讓您在成功提交表單時，傳送電子郵件給一或多個收件者。 此提交動作可讓您建立包含預先定義格式之表單資料的電子郵件。 例如，考慮以下範本，其中從已提交的表單資料中擷取客戶名稱、送貨地址、州名稱和郵遞區號：


    ```
    ${customer_Name} 您好：
    
    以下設定為您的預設送貨地址：
    ${customer_Name},
    ${customer_Shipping_Address},
    ${customer_State},
    ${customer_ZIPCode}
    
    謹此，
    WKND
    ```

## 優點

設定具有「寄送電子郵件」提交動作的最適化表單的一些優點包括：

* 它可讓使用者快速通訊，因為表單資料會直接傳送給指定的電子郵件收件者。
* 其可將表單提交直接整合到電子郵件通知中，因此有助於簡化工作流程。
* 其可協助組織自訂電子郵件內容，從而使其適合特定的通訊需求。

>[!BEGINTABS]

>[!TAB 基礎元件]

若要設定Foundation元件的「傳送電子郵件提交」動作：

1. 開啟最適化表單以進行編輯，並導覽至最適化表單容器屬性的&#x200B;**[!UICONTROL 提交]**&#x200B;區段。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 傳送電子郵件]**。

   傳送電子郵件的![動作設定](/help/forms/assets/send-email-fc.png)

1. 在&#x200B;**[!UICONTROL 寄件者]**&#x200B;文字方塊中指定寄件者的電子郵件識別碼。
1. 在&#x200B;**[!UICONTROL To]**&#x200B;文字方塊中新增收件者的電子郵件識別碼。 您可以按一下&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕，新增多個收件者。
1. [選擇性]按一下&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕，新增副本和密件副本的收件者。
1. 在&#x200B;**[!UICONTROL 主旨]**&#x200B;文字方塊中指定主旨列。
1. 新增電子郵件範本以設定傳送電子郵件提交動作。
   * 您可以使用&#x200B;**[!UICONTROL 外部範本路徑]**&#x200B;選項，指定儲存在AEM資產中的外部電子郵件範本的路徑。
   * 您也可以在&#x200B;**[!UICONTROL 電子郵件範本]**&#x200B;文字方塊中為表單提交新增自訂電子郵件範本。
1. [選擇性] **[!UICONTROL 傳送電子郵件]**&#x200B;提交動作提供選項，可在電子郵件中包含附件和[記錄檔案(DoR)](generate-document-of-record-core-components.md)。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!TAB 核心元件]

若要設定核心元件的「傳送電子郵件提交」動作：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 傳送電子郵件]**。

   傳送電子郵件的![動作設定](/help/forms/assets/send-email-action-configuration.gif)
1. 在&#x200B;**[!UICONTROL 寄件者]**&#x200B;文字方塊中指定寄件者的電子郵件識別碼。
1. 在&#x200B;**[!UICONTROL To]**&#x200B;文字方塊中新增收件者的電子郵件識別碼。 您可以按一下&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕，新增多個收件者。
1. [選擇性]按一下&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕，新增副本和密件副本的收件者。
1. 在&#x200B;**[!UICONTROL 主旨]**&#x200B;文字方塊中指定主旨列。
1. 新增電子郵件範本以設定傳送電子郵件提交動作。
   * 您可以使用&#x200B;**[!UICONTROL 外部範本路徑]**&#x200B;選項，指定儲存在AEM資產中的外部電子郵件範本的路徑。
   * 您也可以在&#x200B;**[!UICONTROL 電子郵件範本]**&#x200B;文字方塊中為表單提交新增自訂電子郵件範本。
1. [選擇性] **[!UICONTROL 傳送電子郵件]**&#x200B;提交動作提供選項，可在電子郵件中包含附件和[記錄檔案(DoR)](generate-document-of-record-core-components.md)。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!TAB 通用編輯器]

若要在Universal Editor中設定傳送電子郵件提交動作：

1. 開啟最適化表單進行編輯。
1. 按一下編輯器上的&#x200B;**編輯表單屬性**擴充功能。
**表單屬性**&#x200B;對話方塊就會顯示。

   >[!NOTE]
   >
   > * 如果您在通用編輯器介面中看不到&#x200B;**編輯表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
   > * 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。


1. 按一下&#x200B;**提交**&#x200B;索引標籤，然後選取&#x200B;**[!UICONTROL 傳送電子郵件]**&#x200B;提交動作。

   ![傳送電子郵件通用編輯器](/help/forms/assets/send-email-ue.png)

1. 在&#x200B;**[!UICONTROL 寄件者]**&#x200B;文字方塊中指定寄件者的電子郵件識別碼。
1. 在&#x200B;**[!UICONTROL To]**&#x200B;文字方塊中新增收件者的電子郵件識別碼。 您可以按一下&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕，新增多個收件者。
1. [選擇性]按一下&#x200B;**[!UICONTROL 新增]**&#x200B;按鈕，新增副本和密件副本的收件者。
1. 在&#x200B;**[!UICONTROL 主旨]**&#x200B;文字方塊中指定主旨列。
1. 新增電子郵件範本以設定傳送電子郵件提交動作。
   * 您可以使用&#x200B;**[!UICONTROL 外部範本路徑]**&#x200B;選項，指定儲存在AEM資產中的外部電子郵件範本的路徑。
   * 您也可以在&#x200B;**[!UICONTROL 電子郵件範本]**&#x200B;文字方塊中為表單提交新增自訂電子郵件範本。
1. [選擇性] **[!UICONTROL 傳送電子郵件]**&#x200B;提交動作提供選項，可在電子郵件中包含附件和[記錄檔案(DoR)](generate-document-of-record-core-components.md)。
1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。

>[!ENDTABS]

## 最佳實務 {#best-practices}

* 建議保持電子郵件內容簡潔明瞭。 使用者應該瞭解電子郵件的用途，以及需要採取的任何動作。
* 建議所有表單欄位都有唯一的元素名稱，即使它們放在調適型表單的不同面板上亦然。
* 使用 AEM as a Cloud Service 時，傳出的電子郵件必須加密。傳出的電子郵件功能預設會停用。若要啟用它，請將支援票證提交至[要求存取權](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html?lang=zh-Hant#sending-email)。

## 相關文章

{{af-submit-action}}
