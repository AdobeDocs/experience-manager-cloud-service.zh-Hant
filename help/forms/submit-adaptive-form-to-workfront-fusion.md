---
title: 整合Adobe Workfront Fusion與AEM Forms提交作業
description: Adobe Workfront Fusion可讓您專注於新工作，而非重複工作。 您可以使用表單提交功能將Adobe Workfront Fusion連結至最適化表單。
keywords: 提交最適化表單至Adobe Workfront Fusion、Adobe Workfront Fusion與AEM Forms提交的整合、Adobe Workfront Fusion與AEM Forms、Workfront Fusion與AEM Forms、連線Workfront Fusion至AEM Forms、AEM Forms及Workfront Fusion、如何連線Workfront Fusion與AEM Forms？，連線Workfront Fusion至表單
topic-tags: author, developer
feature: Adaptive Forms
role: Admin, User
exl-id: d3efb450-a879-40ae-8958-0040f99bdafc
source-git-commit: 975f767e75a268a1638227ae20a533f82724c80a
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 3%

---

# 向 Adobe Workfront Fusion 提交最適化表單

<span class="preview"> 此功能可在早期採用者計畫下取得。 您可以從您的官方電子郵件ID寫信到aem-forms-early-adopter-program@adobe.com ，以加入率先採用者計畫並請求存取該功能。 </span>

[Adobe Workfront Fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) 自動化重複相同工作的程式，例如檔案核准工作流程、電子郵件篩選和排序，讓您專注在新工作上，而非重複工作。 Adobe Workfront Fusion包含多個情境。 案例由一系列模組組成，這些模組會在應用程式和Web服務之間執行資料傳輸。 在案例中，您會新增各種步驟（模組）來自動化工作。

例如，使用Workfront Fusion，您可以建立案例來透過Adaptive Form收集資料、處理資料，以及傳送資料至資料存放區進行封存。 一旦設定了案例，每當使用者填寫表單時，Workfront Fusion就會自動執行工作，順暢地更新資料存放區。

## 使用Adobe Workfront Fusion的優勢{#advatages-of-workfront-fusion}

將Adobe Workfront Fusion與AEM Forms搭配使用的一些優點：

- 將最適化Forms擷取的資料傳送到Workfront Fusion情境
- 將容易發生錯誤的工作自動化。
- 自訂組織的特定需求，這些需求未直接包含在Workfront中。
- 處理簡單的邏輯和直接的決定，例如if/then陳述式。

## 整合AEM Forms與Adobe Workfront Fusion的必要條件 {#prerequisites}

將Workfront Fusion連線至AEM Forms所需的先決條件為：

- 有效的 [Workfront Fusion授權](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/license-automation-vs-integration.html).
- 具有存取許可權的AEM使用者 [開發主控台](https://my.cloudmanager.adobe.com/) 至 [擷取服務認證](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html).

## 將AEM Forms與Adobe Workfront Fusion整合

若要連線 [Workfront fusion](https://experienceleague.adobe.com/docs/workfront/using/adobe-workfront-fusion/get-started-with-workfront-fusion/workfront-fusion-overview.html) 若要建立表單，請執行下列步驟：

### 1.建立Workfront情境 {#workflow-scenario}

若要建立Workfront情境：
1. 登入您的 [Workfront Fusion帳戶](https://app-qa.workfrontfusion.com/).
1. 按一下 **[!UICONTROL 情境]** ![「共用」圖示](/help/forms/assets/Smock_ShareAndroid_18_N.svg) 在左側面板中。
1. 按一下 **[!UICONTROL 建立新情境]** 在頁面的右上角。 建立新情境的頁面會顯示在畫面上。
1. 選取 **[!UICONTROL 新情境]** 在頁面的左上角，為案例輸入正確的名稱。
1. 按一下問號，並確定您將第一個模組新增為 **[!UICONTROL AEM Forms]**.

   ![新增AEM Forms模組](/help/forms/assets/workfront-aemforms.png)

   此 **[!UICONTROL 關注表單事件]** 對話方塊隨即顯示。

   >[!NOTE]
   >
   > 第一個模組必須新增為 **[!UICONTROL AEM Forms]**.

1. 選取 **[!UICONTROL 關注表單事件]** 對話方塊與新增webhook的視窗隨即出現。

#### 1.1新增webhook {#add-webhook}

![新增webhook](/help/forms/assets/workfront-add-webhook.png)

若要新增webhook：

1. 按一下 **[!UICONTROL 新增]** 和 **[!UICONTROL 新增webhook]** 對話方塊隨即顯示。
1. 指定webhook名稱。

   >[!NOTE]
   >
   > 建議您謹慎選擇您的webhook名稱，因為指定的webhook名稱會顯示在AEM執行個體中。

1. 按一下 **[!UICONTROL 新增]** 以新增連線。 此 **[!UICONTROL 建立連線]** 對話方塊隨即顯示。

#### 1.2將連線新增至webhook {#add-connection}

![新增連線](/help/forms/assets/workfront-add-connection.png)

若要新增連線：

1. 指定 **[!UICONTROL 連線名稱]** 在 **[!UICONTROL 建立連線]** 對話方塊。

1. 選取 **環境** 和 **型別** 下拉式清單中的。

1. 輸入 **執行個體URL**.

   >[!NOTE]
   >
   > 執行個體URL是指向特定AEM Forms執行個體的唯一網址。

   您可以擷取 [來自開發人員控制檯的服務認證](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials.html) 建立連線時需要。

1. 取代 `ims-na1.adobelogin.com` 在 **IMS端點** ，值為 **imsEndpoint** 從開發人員控制檯中的服務認證。

   >[!NOTE]
   >
   > 保留 `https://` 在 **IMS端點** 文字方塊 `imsEndpoint` URL。

1. 在 **[!UICONTROL 建立連線]** 對話方塊：
   - 指定 **使用者端ID** 具有值 **clientId** 從開發人員控制檯中的服務認證。
   - 指定 **使用者端密碼** 具有值 **使用者端密碼** 從開發人員控制檯中的服務認證。
   - 指定 **技術帳戶ID**  具有值 **id** 從開發人員控制檯中的服務認證。
   - 指定 **組織ID**  具有值 **org** 從開發人員控制檯中的服務認證。
   - **中繼範圍**  具有值 **metascope** 從開發人員控制檯中的服務認證。
   - **私密金鑰**  具有值 **privateKey** 從開發人員控制檯中的服務認證。

   >[!NOTE]
   >
   >- 的 **私密金鑰**，移除 `\r\n` 從它的值開始。
   >  例如，如果私密金鑰值為：
   >`\r\nIJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL\r\nMy1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`，然後在移除 `\r\n` 從私密金鑰來看，金鑰看起來類似這樣，兩個值都出現在單獨的一行中：
   >
   >   `IJAVO8GDYAOZ9jMA0GCSqGSIb3DQEBCwUAMDAxL`
   >
   >   `My1lMTUxODMxLWNtc3RnLWludGVncmF0aW9uLTAw`
   > 
   >- 您還可以選擇選取 **Extract** 按鈕。

1. 按一下&#x200B;**「繼續」**。

   建立的連線會開始出現在 **[!UICONTROL 連線]** 在 **[!UICONTROL 新增webhook]** 對話方塊。

1. 選取建立的連線 **[!UICONTROL 連線]** 下拉式清單中的。
1. 按一下「**[!UICONTROL 儲存]**」。
1. 按一下 **[!UICONTROL 確定]** 並儲存情境的變更。

#### 1.3啟動Workfront情境 {#activate-scenario}

若要啟動案例：

1. 按一下 **[!UICONTROL 情境]** ![「共用」圖示](/help/forms/assets/Smock_ShareAndroid_18_N.svg) 在左側面板中。
1. 按一下 **[!UICONTROL 非使用中案例]** 標籤。
1. 按一下 **開啟/關閉** 適用於您的AEM Forms情境的切換按鈕。

按一下切換按鈕後， Workfront案例就會開始出現在 **[!UICONTROL 作用中情境]** 標籤。

>[!NOTE]
>
> 如果您未啟用Workfront案例，其不會偵測表單提交，且將提交動作設定為Workfront會導致提交失敗。

### 2.設定Workfront Fusion適用性表單的提交動作

您可以為Workfont Fusion設定提交動作：
- [全新最適化Forms](#new-af-submit-action)
- [現有的最適化表單](#existing-af-submit-action)

#### 設定Workfront Fusion適用性表單的提交動作 {#new-af-submit-action}

若要設定Workfront Fusion適用性表單的提交動作：

1. 登入您的AEM執行個體。
1. 前往 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]** > **[!UICONTROL 建立]** > **[!UICONTROL 最適化表單]**. 此 **[!UICONTROL 建立表單]** 精靈出現。
1. 選擇最適化表單範本，從 **[!UICONTROL 來源]** 標籤。
1. 從中選擇主題 **[!UICONTROL 樣式]** 標籤。

   ![適用於Workfront Fusion的提交動作](/help/forms/assets/workfront-scenario-new-af.png)

1. 選取 **[!UICONTROL 叫用Workfront Fusion案例]** 從 **[!UICONTROL 提交]** 標籤。
1. 從中選擇已建立的webhook **[!UICONTROL 選項]** 索引標籤中的 **[!UICONTROL 屬性]** 視窗。

   >[!NOTE]
   >
   > Workfront情境的webhook名稱會顯示在 **選項** 下拉式清單。

1. 按一下&#x200B;**[!UICONTROL 建立]**。
1. 指定新最適化表單的名稱，然後按一下 **[!UICONTROL 建立]**.

#### 設定Workfront Fusion現有最適化表單的提交動作 {#existing-af-submit-action}

若要設定Workfront Fusion現有最適化表單的提交動作：

1. 登入您的AEM執行個體。
1. 前往 **[!UICONTROL Forms]** > **[!UICONTROL Forms與檔案]**.
1. 選取最適化表單，然後在編輯模式中開啟表單。
1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。

   ![適用於Workfront Fusion的提交動作](/help/forms/assets/workfront-scenario-existing-af.png)

1. 開啟 **[!UICONTROL 提交]** 標籤。
1. 選取 **[!UICONTROL 提交動作]** 作為 **[!UICONTROL 叫用Workfront Fusion案例]**
1. 選取 **[!UICONTROL Workfront Fusion分析藍本]** 下拉式清單中的。
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

## 最佳做法 {#best-practices}

- 建議您謹慎選擇您的webhook名稱，因為在AEM執行個體無法取得案例名稱。 如果您日後變更webhook名稱，則不會反映在AEM Forms提交動作下拉式清單中。
- 一個案例可以有多個webhook連結，但一次只能有一個webhook連結處於作用中。 建議刪除未連結的webhook，使其不會出現在AEM Forms提交動作下拉式清單中。

<!-- During testing or development of Workfront, add the Author URL to the instance URL. However, when deploying Workfront Fusion in a production environment, it is recommended to replicate the scenario URLs for the Publish instance. -->
