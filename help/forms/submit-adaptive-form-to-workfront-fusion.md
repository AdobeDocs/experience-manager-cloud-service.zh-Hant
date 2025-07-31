---
title: 整合Adobe Workfront Fusion與AEM Forms提交作業
description: Adobe Workfront Fusion可讓您專注於新工作，而非重複工作。 您可以使用表單提交功能將Adobe Workfront Fusion連結至最適化表單。
keywords: 提交最適化表單至Adobe Workfront Fusion、Adobe Workfront Fusion與AEM Forms提交的整合、Adobe Workfront Fusion與AEM Forms、Workfront Fusion與AEM Forms、連線Workfront Fusion至AEM Forms、AEM Forms及Workfront Fusion、如何連線Workfront Fusion與AEM Forms？，連線Workfront Fusion至表單
topic-tags: author, developer
feature: Adaptive Forms, Foundation Components, Edge Delivery Services, Core Components
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '1287'
ht-degree: 4%

---

# 向 Adobe Workfront Fusion 提交最適化表單

<span class="preview">此功能可在早期採用者方案下使用。 您可以從您的官方電子郵件ID寫信到aem-forms-ea@adobe.com ，以加入率先採用者計畫並請求存取該功能。</span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html)會自動執行重複相同工作的程式，例如檔案核准工作流程、電子郵件篩選和排序，讓您專注在新工作上，而非重複工作。 Adobe Workfront Fusion包含多個情境。 案例由一系列模組組成，這些模組會在應用程式和Web服務之間執行資料傳輸。 在案例中，您會新增各種步驟（模組）來自動化工作。

例如，使用Workfront Fusion，您可以建立案例來透過Adaptive Form收集資料、處理資料，以及傳送資料至資料存放區進行封存。 一旦設定了案例，每當使用者填寫表單時，Workfront Fusion就會自動執行工作，順暢地更新資料存放區。

AEM Forms as a Cloud Service提供OOTB聯結器，可連線最適化表單並將其提交至Adobe Workfront Fusion。 將表單提交至Adobe Workfront Fusion有幾項好處：
* 它可讓表單提交資料順暢地傳輸至Workfront Fusion工作流程。
* 它有助於自動執行由表單提交觸發的各種任務。 這可以包括起始專案、指派任務給特定團隊成員、傳送通知以及更新專案狀態 — 所有這一切都不需要手動介入。
* 所有在Workfront Fusion中擷取的表單提交內容，都提供專案相關資訊的單一信任來源


<!--  AEM as a Cloud Service offers various out of the box submit actions for handling form submissions. You can learn more about these options in the [Adaptive Form Submit Action](/help/forms/configure-submit-actions-core-components.md)  article.-->

>[!VIDEO](https://video.tv.adobe.com/v/3427145/adaptive-forms-adobe-workfront-af-workfront-workfront-aem-forms/?quality=12&learn=on)

## 整合AEM Forms與Adobe Workfront Fusion的必要條件 {#prerequisites}

若要在Workfront Fusion和AEM Forms之間建立連線，需具備下列條件：

* 有效的[Workfront和Workfront Fusion授權](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html)。
* 有權存取[開發主控台](https://my.cloudmanager.adobe.com/)以[擷取服務認證](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)的AEM使用者。

## 將AEM Forms與Adobe Workfront Fusion整合

### 1.建立Workfront情境 {#workflow-scenario}

若要建立Workfront案例，請執行下列步驟：

1. [建立情境](#create-scenario)
1. [將Web勾點新增至情境](#add-webhook)
1. [將連線新增至Web鉤點](#add-connection)

#### 建立情境 {#create-scenario}

若要建立情境：

1. 登入您的[Workfront Fusion帳戶](https://app-qa.workfrontfusion.com/)。
1. 按一下左側面板中的&#x200B;**[!UICONTROL 情境]** ![共用圖示](/help/forms/assets/Smock_ShareAndroid_18_N.svg)。
1. 按一下頁面右上角的&#x200B;**[!UICONTROL 建立新案例]**。 建立新情境的頁面會顯示在畫面上。
1. 在頁面的左上角選取&#x200B;**[!UICONTROL 新案例]**，然後為案例輸入適當的名稱。
1. 按一下問號，並確認您將第一個模組新增為&#x200B;**[!UICONTROL AEM Forms]**。

   ![新增AEM Forms模組](/help/forms/assets/workfront-aemforms.png)

   **[!UICONTROL 檢視表單事件]**&#x200B;對話方塊就會顯示。

   >[!NOTE]
   >
   > 必須將第一個模組新增為&#x200B;**[!UICONTROL AEM Forms]**。

1. 選取「**[!UICONTROL 關注表單事件]**」對話方塊，就會顯示新增webhook的視窗。

#### 新增webhook {#add-webhook}

![新增webhook](/help/forms/assets/workfront-add-webhook.png)

若要新增webhook：

1. 按一下「**[!UICONTROL 新增]**」並出現「**[!UICONTROL 新增webhook]**」對話方塊。
1. 指定webhook名稱。

   >[!NOTE]
   >
   > 建議您謹慎選擇您的webhook名稱，因為指定的webhook名稱會顯示在AEM例項中。

1. 按一下&#x200B;**[!UICONTROL [新增]**]以新增連線。 **[!UICONTROL 建立連線]**&#x200B;對話方塊就會顯示。

>[!NOTE]
>
> 請確定技術帳戶是&#x200B;**forms-users**&#x200B;群組的成員；否則，新增webhook會失敗。

#### 新增與webhook的連線 {#add-connection}

![新增連線](/help/forms/assets/workfront-add-connection.png)

若要新增連線：

1. 在&#x200B;**[!UICONTROL 建立連線]**&#x200B;對話方塊中指定&#x200B;**[!UICONTROL 連線名稱]**。

1. 從下拉式清單中選取&#x200B;**環境**&#x200B;和&#x200B;**型別**。

1. 輸入&#x200B;**執行個體URL**。

   >[!NOTE]
   >
   > 執行個體URL是指向特定AEM Forms執行個體的唯一網址。

   您可以從建立連線所需的開發人員主控台[擷取](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html)服務認證。

1. 從開發人員主控台中的服務認證中，將`ims-na1.adobelogin.com`IMS端點&#x200B;**中的**&#x200B;取代為&#x200B;**imsEndpoint**&#x200B;的值。

   >[!NOTE]
   >
   > 新增`https://` URL時，保留&#x200B;**IMS端點**&#x200B;文字方塊中的`imsEndpoint`。

1. 在&#x200B;**[!UICONTROL 建立連線]**&#x200B;對話方塊中指定下列值：
   * 從開發人員主控台中的服務認證中指定值為&#x200B;**clientId**&#x200B;的&#x200B;**使用者端識別碼**。
   * 從開發人員主控台中的服務認證中指定值為&#x200B;**clientSecret**&#x200B;的&#x200B;**使用者端密碼**。
   * 從開發人員主控台中的服務認證指定&#x200B;**技術帳戶ID** （值為&#x200B;**ID**）。
   * 從開發人員主控台中的服務認證中指定值為&#x200B;**org**&#x200B;的&#x200B;**組織ID**。
   * 開發人員主控台中服務認證值為&#x200B;**中繼領域**&#x200B;的&#x200B;**中繼領域**。
   * 從開發人員主控台中的服務認證取得值為&#x200B;**privateKey**&#x200B;的&#x200B;**私密金鑰**。

   >[!NOTE]
   >
   >* 針對&#x200B;**私密金鑰**，從其值移除`\r\n`。
   >  例如，如果私密金鑰值為：
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`，然後從私密金鑰中移除`\r\n`後，金鑰看起來會像這樣，而且這兩個值都會出現在單獨的一行中：
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >* 您也可選擇選取&#x200B;**擷取**&#x200B;按鈕，以擷取檔案中的私密金鑰或憑證。

1. 按一下「**繼續**」。

   建立的連線開始出現在&#x200B;**[!UICONTROL 新增webhook]**&#x200B;對話方塊的&#x200B;**[!UICONTROL 連線]**&#x200B;的下拉式清單中。

1. 從下拉式清單中選取已建立的連線&#x200B;**[!UICONTROL 連線]**。
1. 按一下「**[!UICONTROL 儲存]**」。
1. 按一下&#x200B;**[!UICONTROL 確定]**&#x200B;並儲存情境的變更。
1. 若要啟用情境，請按一下情境編輯器中的開啟/關閉切換按鈕。

>[!NOTE]
>
> 如果您未啟用Workfront案例，其不會偵測表單提交，且將提交動作設定為Workfront會導致提交失敗。

### 2.設定Workfront Fusion適用性表單的提交動作

>[!BEGINTABS]

>[!TAB 基礎元件]

若要根據Workfront Fusion的基礎元件設定最適化表單的提交動作：

1. 開啟最適化表單以進行編輯，並導覽至最適化表單容器屬性的&#x200B;**[!UICONTROL 提交]**&#x200B;區段。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 叫用Workfront Fusion案例]**。
   ![Workfront Fusion的提交動作](/help/forms/assets/workfront-fusion-fc.png)

1. 從下拉式清單中選取&#x200B;**[!UICONTROL Workfront Fusion案例]**。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。


>[!TAB 核心元件]

若要根據Workfront Fusion的核心元件設定最適化表單的提交動作：

1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從&#x200B;**[!UICONTROL 提交動作]**&#x200B;下拉式清單中，選取&#x200B;**[!UICONTROL 叫用Workfront Fusion案例]**。

   ![Workfront Fusion的提交動作](/help/forms/assets/workfront-scenario-existing-af.png)
1. 從下拉式清單中選取&#x200B;**[!UICONTROL Workfront Fusion案例]**。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!TAB 通用編輯器]

若要設定使用通用編輯器編寫的最適化表單的提交動作：

1. 開啟最適化表單進行編輯。
1. 按一下編輯器上的&#x200B;**編輯表單屬性**擴充功能。
**表單屬性**&#x200B;對話方塊就會顯示。

   >[!NOTE]
   >
   > * 如果您在通用編輯器介面中看不到&#x200B;**編輯表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
   > * 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。

1. 按一下「**提交**」標籤，然後選取「**[!UICONTROL 叫用Workfront Fusion案例]**」提交動作。

   ![Workfront Fusion的提交動作](/help/forms/assets/workfront-fusion-ue.png)

1. 從下拉式清單中選取&#x200B;**[!UICONTROL Workfront Fusion案例]**。
1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。

>[!ENDTABS]

## 最佳實務 {#best-practices}

* 建議您謹慎選擇您的webhook名稱，因為在AEM例項中無法取得案例名稱。 如果您日後變更webhook名稱，則不會反映在AEM Forms提交動作下拉式清單中。
* 一個案例可以有多個webhook連結，但一次只能有一個webhook連結處於作用中。 建議刪除未連結的webhook，使其不會出現在AEM Forms提交動作下拉式清單中。

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->

## 相關文章

{{af-submit-action}}