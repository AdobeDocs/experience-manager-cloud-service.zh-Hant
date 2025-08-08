---
title: 如何將Marketo Engage與AEM Forms整合？
description: 瞭解如何將Marketo Engage執行個體與AEM Forms整合。
keywords: 如何連結Marketo執行個體與表單？、將表單連線至Marketo、將表單與Marketo Engage整合、將調適型表單與Marketo執行個體整合。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 74cd25f9-1ee1-4f3f-8e02-8714071e7c86
source-git-commit: 1be7bafc1d93a65a81eeb2f7e86cac33cde7aa35
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 3%

---

# 將 Marketo Engage 與 AEM Forms 進行整合

<span class="preview">此功能可在早期採用者方案下使用。 您可以從您的官方電子郵件ID寫信到aem-forms-ea@adobe.com ，以加入率先採用者計畫並請求存取該功能。</span>

將AEM Forms與[Adobe Marketo Engage](https://experienceleague.adobe.com/zh-hant/docs/marketo/using/home)整合可讓使用者運用Marketo Engage的功能，從擷取的資料建立商業邏輯，並自動化工作流程，包括智慧行銷活動和電子郵件自動化。 設定的表單可以將擷取的資料傳送到Marketo Engage進行處理。

## 將Marketo Engage與表單整合的優點

以下是將AEM表單與Adobe Marketo Engage連結的一些優點：

* **簡化整合**：將表單與Marketo Engage連線後，就不需要建立個別的表單資料模型。 整合程式簡單明瞭，且方便使用。
* **自動資料擷取**：它有助於自動擷取表單提交並將它們儲存在Marketo中，消除手動資料輸入並減少錯誤。

* **銷售機會管理**：它會將表單提交直接整合到行銷資料庫，以便更好地追蹤和培養銷售機會，藉此簡化銷售機會管理流程。

* **改善行銷活動績效**：它使用表單資料來分析和最佳化行銷活動，提高整體績效和投資報酬率(ROI)。

* **分析和報告**：它有助於在Marketo中存取強大的分析和報告工具，例如Munchkin，以評估表單和行銷活動的有效性。

* **後續作業自動化**：它有助於自動化後續作業電子郵件以及表單提交所觸發的工作流程，確保與潛在客戶進行及時溝通。

## 使用AEM Forms勝過其他表單解決方案的主要優點

下表概述選擇AEM Forms勝過其他替代表單解決方案的幾個原因：

| **功能** | **AEM Forms** | **其他表單解決方案** |
|-------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------|
| **自訂** | 允許新增特定自訂功能、調整表單動作和修改欄位行為以增強表單互動、複雜的工作流程 | 不支援自訂 |
| **規則編輯器** | 支援內建規則編輯器，可新增邏輯和條件。 | 不支援規則編輯器 |
| **配置選項** | 支援多個版面選項 | 有限的版面配置選項 |
| **預填服務** | 提供預填服務以自動填入表單資料。 | 沒有可用的預填服務 |
| **嵌入網站** | 可使用iFrame嵌入網站中 | 無法使用iFrame內嵌在網站中 |
| **輕鬆與網站整合** | 無需額外學習；AEM Forms使用與Sites相同的技能 | 可能需要額外學習 |
| **資料提交** | 可將資料提交至各種平台，並提供多個聯結器，例如連線至SharePoint、連線至OneDrive、連線至Salesforce等。 | 可將資料提交至有限的聯結器，例如提交至Salesforce |

## 將Marketo Engage與表單整合的考量事項

整合Marketo Engage與AEM Forms時的一些考量事項：

* AEM僅支援各種Marketo資料庫中的People (Leads)資料庫。
* Marketo允許建立[10個自訂物件](https://experienceleague.adobe.com/zh-hant/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields)作為使用者定義的物件，以儲存潛在客戶中標準欄位以外的專門資料，支援獨特的業務需求。
* AEM只能存取與Lead資料庫相關聯的自訂物件

## 將Marketo Engage與表單整合的先決條件

以下是連線Marketo Engage與AEM Forms的先決條件：

* 有效的Adobe Marketo Engage授權
* 用於[擷取使用者端ID和使用者端密碼](https://experienceleague.adobe.com/zh-hant/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api)以建立雲端設定的Marketo Engage工作執行個體。

## 建立雲端服務設定以連線AEM Forms (Adaptive Forms)與Marketo Engage

![工作流程](/help/forms/assets/workflow-marketo-1.png)

>[!VIDEO](https://video.tv.adobe.com/v/3442865/engage-marketo-aem-forms-aem)

<span>此影片僅適用於核心元件。 若為UE/Foundation元件，請參閱文章。</span>

雲端設定會將您的Experience Manager執行個體連線至Adobe Marketo Engage執行個體。 執行以下步驟來建立Marketo Engage雲端設定：

1. 移至&#x200B;**工具** > **雲端服務** > **Marketo Engage**。

   ![Marketo Engage](/help/forms/assets/marketo-engage.png)

2. 開啟資料夾以裝載組態，然後按一下[建立]。**&#x200B;** **建立Marketo Engage組態**&#x200B;視窗會出現。

   >[!NOTE]
   >
   > 您也可以[設定雲端服務設定的資料夾](/help/forms/configure-data-sources.md#configure-folder-for-cloud-service-configurations)。

3. 指定組態的&#x200B;**標題**&#x200B;和要連線至服務的認證。 您可以從Adobe Marketo Engage儀表板擷取驗證認證：
   * **使用者端識別碼**&#x200B;和&#x200B;**使用者端密碼**&#x200B;可在&#x200B;**管理員** > **整合** > **LaunchPoint**&#x200B;中使用，方法是選取自訂服務並按一下&#x200B;**檢視詳細資料**。
   * **身分URL**&#x200B;可在&#x200B;**管理員** > **整合** > **網頁服務**&#x200B;中使用，在&#x200B;**REST API**&#x200B;區段中做為&#x200B;**身分**。

4. 按一下&#x200B;**連線**。  連結成功後，就會顯示 `Authentication Successful` 訊息。
5. 按一下&#x200B;**[!UICONTROL 建立]**&#x200B;以儲存雲端組態設定。

![Marketo Engage雲端設定](/help/forms/assets/marketo-engage-cloud-configuration.png)

現在您可以使用建立的雲端服務設定，將Marketo Engage資料來源連線至最適化表單。

## 下一步

您已建立雲端服務設定來整合Adobe Marketo Engage與AEM Forms。 現在，您可以整合：
* [使用Marketo Engage建立最適化表單](/help/forms/integrate-adaptive-form-with-marketo-engage.md)
* [使用Marketo Engage的現有最適化表單](/help/forms/use-marketo-engage-data-source-in-form.md)

## 相關的文章

{{af-submit-action}}

## 另請參閱

{{marketo-engage-see-also}}
