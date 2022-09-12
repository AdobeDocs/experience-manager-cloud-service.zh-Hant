---
title: 將最適化表單與Microsoft®電源自動化整合
description: 將適用性表單與Microsoft® Power自動化整合。
hide: true
hidefromtoc: true
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
source-git-commit: ccc4d487cb180273284276cf9cdf18680a3efcb8
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 1%

---

# 使用Microsoft® Power Automate連接最適化表單 {#connect-adaptive-form-with-power-automate}

您可以設定適用性表單，在提交時執行Microsoft® Power Automate Cloud Flow。 配置的適用性表單會將捕獲的資料、附件和記錄文檔發送到Power Automate Cloud Flow進行處理。 它可協助您建立自訂資料擷取體驗，同時運用Microsoft® Power Automate的強大功能，圍繞擷取的資料建立業務邏輯，並自動化客戶工作流程。 以下是整合適用性表單與Microsoft®電源自動化後，您可以做的事：

* 在強大的自動化業務流程中使用自適應Forms資料
* 使用Power Automate將捕獲的資料發送到500多個資料源或任何公開可用的API
* 對捕獲的資料執行複雜計算
* 按照預定義的時間表將適用性Forms資料保存到儲存系統

適用性Forms編輯器提供 **調用Microsoft®電源自動流** 傳送最適化表單資料、附件和記錄檔的提交動作會傳送至Power Automate Cloud Flow。 要使用「提交」操作將捕獲的資料發送到Microsoft® Power Automate, [使用Microsoft® Power Automate連接您的Formsas a Cloud Service實例](forms-microsoft-power-automate-integration.md#connect-forms-server-with-power-automate)

## 必備條件

使用Microsoft® Power Automate連接適用性表單時需要執行下列操作：

* Microsoft® Power Automate Premium授權。
* Microsoft® [電源自動流](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) 和 `When an HTTP request is received` 觸發以接受適用性表單提交資料。


* 具有Forms作者和Forms管理員權限的Experience Manager使用者。
* 確保用於連接到Power Automate的帳戶是Power Automate流的所有者。


## 使用Microsoft® Power Automate連接您的Formsas a Cloud Service實例 {#connect-forms-server-with-power-automate}

執行下列動作，使用Forms® Power Automate連線您的Microsoftas a Cloud Service執行個體：

1. 建立Microsoft® Azure Active Directory應用程式
1. 建立Microsoft® Power Automate Dataverse Cloud配置。
1. 建立Microsoft® Power Automate Flow Service Cloud配置
1. 發佈Microsoft® Power自動化Dataverse Cloud設定。

### 建立Microsoft® Azure Active Directory應用程式 {#ms-power-automate-application}

1. 登入 [Azure門戶](https://portal.azure.com/).
1. 選擇 [!UICONTROL Azure Active Directory] 從左側導覽。
1. 在「預設目錄」頁上，選擇 [!UICONTROL 應用程式註冊] 從左側面板。
1. 在「應用程式註冊」頁面上，按一下「新註冊」。
1. 在頁面上指定名稱、支援的帳戶類型和重定向URI。 在重定向URI中，指定以下內容，然後按一下「保存」。
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![註冊Azure Active Directory應用程式](assets/power-automate-application.png)

   >[!NOTE]
   >如有必要，您也可以從「驗證」頁指定其他重定向URI。
   > 針對支援的帳戶類型，請根據您的使用案例選取單一租用戶、多個租戶或個人Microsoft帳戶


1. 在「驗證」頁上，啟用以下選項，然後按一下「保存」。


   * 存取權杖（用於隱式流量）
   * ID代號（用於隱式和混合式流程）

1. 在API權限頁面上，按一下新增權限。
1. 在Microsoft® API下，選取「流量服務」並選取下列權限。
   * Flows.Manage.All
   * Flows.Read.All

   按一下「新增權限」以儲存權限。
1. 在API權限頁面上，按一下新增權限。 選取我的組織使用和搜尋的API `DataVerse`.
1. 啟用user_impersonation並按一下添加權限。
1. （選用）在「憑證與機密」頁面上，按一下「新增用戶端密碼」 。 在新增用戶端密碼畫面中，提供密碼過期的說明和時段，然後按一下新增。 產生機密字串。
1. 請保留貴組織的特定備注 [Dynamics環境URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests).

### 建立Microsoft®電源自動化Dataverse Cloud配置 {#microsoft-power-automate-dataverse-cloud-configuration}

1. 在AEM Forms作者例項上，導覽至 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 配置瀏覽器]**.
1. 在 **[!UICONTROL 配置瀏覽器]** 頁面，點選 **[!UICONTROL 建立]**.
1. 在 **[!UICONTROL 建立配置]** 對話框，指定 **[!UICONTROL 標題]** 若為設定，請啟用 **[!UICONTROL 雲端設定]**，然後點選 **[!UICONTROL 建立]**. 這樣便會建立儲存 Cloud Services 的設定容器。請確保資料夾名稱未含任何空格。
1. 導覽至 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** 並開啟您在上一步驟中建立的設定容器。

   >[!NOTE]
   >
   >建立適用性表單時，請在 **[!UICONTROL 組態容器]** 欄位。
1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL Microsoft® Power Automate Flow Service] 設定(在AEM Forms中)。
1. 在 **[!UICONTROL 為Microsoft®電源自動化配置Dataverse Service]** 頁面，指定 **[!UICONTROL 用戶端ID]** （亦稱為應用程式ID）, **[!UICONTROL 用戶端密碼]**, **[!UICONTROL OAuth URL]** 和 **[!UICONTROL 動態環境URL]**. 使用的用戶端ID、用戶端密碼、OAuth URL和動態環境URL [Microsoft® Azure Active Directory應用程式](#ms-power-automate-application) 您在上一節中建立。 在Microsoft® Azure Active Directory應用程式UI中使用端點選項可查找OAuth URL

![Microsoft Power自動化應用程式UI中的「使用端點」選項可尋找OAuth URL](assets/endpoints.png)
Microsoft® Power Automate應用程式UI中的「使用端點」選項可尋找OAuth URL

1. 點選 **[!UICONTROL Connect]** . 如有詢問，請登入您的Microsoft® Azure帳戶。 點選 **[!UICONTROL 儲存]**.

### 建立Microsoft® Power Automate Flow Service Cloud配置。

1. 導覽至 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Flow Service]** 並開啟您在上一節中建立的設定容器。

   >[!NOTE]
   >
   >建立適用性表單時，請在 **[!UICONTROL 組態容器]** 欄位。
1. 在設定頁面上，點選 **[!UICONTROL 建立]** 建立 [!DNL Microsoft® Power Automate Flow Service] 設定(在AEM Forms中)。
1. 在 **[!UICONTROL 配置Microsoft®電源自動化]** 頁面，指定 **[!UICONTROL 用戶端ID]** （亦稱為應用程式ID）, **[!UICONTROL 用戶端密碼]**, **[!UICONTROL OAuth URL]** 和 **[!UICONTROL 動態環境URL]**. 使用用戶端ID、用戶端密碼、OAuth URL和Dynamics環境ID。 在Microsoft® Azure Active Directory應用程式UI中使用端點選項可尋找OAuth URL。 開啟 [我的流程](https://us.flow.microsoft.com) 連結並點選「我的流」，使用URL中列出的ID做為Dynamics Environment ID。
1. 點選 **[!UICONTROL Connect]**. 如有詢問，請登入您的Microsoft® Azure帳戶。 點選 **[!UICONTROL 儲存]**.

### 同時發佈Microsoft® Power Automate Dataverse和Microsoft® Power Automate Flow Service Cloud設定 {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. 導覽至 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power Automate Dataverse]** 並開啟您在上一個 [建立Microsoft®電源自動化Dataverse Cloud配置](#microsoft-power-automate-dataverse-cloud-configuration) 區段。
1. 選取 `dataverse` 設定與點選 **[!UICONTROL 發佈]**.
1. 在「發佈」頁面上，選取 **[!UICONTROL 所有配置]** 點選 **[!UICONTROL 發佈]**. 同時發佈Power Automate Dataverse和Power Automate Flow Service雲配置。

您的Formsas a Cloud Service執行個體現在已與Microsoft® Power Automate連線。 您現在可以將適用性Forms資料傳送至Power Automate流程。

## 使用調用Microsoft®電源自動流提交操作將資料發送到電源自動流 {#use-the-invoke-microsoft-power-automate-flow-submit-action}

在 [使用Microsoft® Power Automate連接您的Formsas a Cloud Service實例](#connect-forms-server-with-power-automate)，請執行下列動作來設定您的最適化表單，以便在表單提交時將擷取的資料傳送至Microsoft®流程。

1. 登入您的Author例項，選取您的最適化表單，然後按一下 **[!UICONTROL 屬性]**.
1. 在「設定容器」中，瀏覽並選取在區段中建立的容器 [建立Microsoft®電源自動化Dataverse Cloud配置](#microsoft-power-automate-dataverse-cloud-configuration)，然後點選 **[!UICONTROL 儲存並關閉]**.
1. 開啟最適化表單以進行編輯並導覽至 **[!UICONTROL 提交]** 區段（「最適化表單容器」屬性）。
1. 在屬性容器中， **[!UICONTROL 提交操作]** 選取 **[!UICONTROL 調用電源自動流]** 選項。 可用電源自動化流程清單可供使用 **[!UICONTROL 電源自動流]** 選項。 選取所需的流程，並在提交時提交最適化Forms資料。

![配置提交操作](assets/submission.png)

>[!NOTE]
>
> 提交最適化表單之前，請確定 `When an HTTP Request is received` 以下JSON結構的觸發程式會新增至您的Power Automate流程。

```
        {
            "type": "object",
            "properties": {
                "attachments": {
                    "type": "array",
                    "items": {
                        "type": "object",
                        "properties": {
                            "filename": {
                                "type": "string"
                            },
                            "data": {
                                "type": "string"
                            },
                            "contentType": {
                                "type": "string"
                            },
                            "size": {
                                "type": "integer"
                            }
                        },
                        "required": [
                            "filename",
                            "data",
                            "contentType",
                            "size"
                        ]
                    }
                },
                "templateId": {
                    "type": "string"
                },
                "templateType": {
                    "type": "string"
                },
                "data": {
                    "type": "string"
                },
                "document": {
                    "type": "object",
                    "properties": {
                        "filename": {
                            "type": "string"
                        },
                        "data": {
                            "type": "string"
                        },
                        "contentType": {
                            "type": "string"
                        },
                        "size": {
                            "type": "integer"
                        }
                    }
                }
            }
        }
```

