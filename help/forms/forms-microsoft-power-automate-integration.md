---
title: 與Microsoft® Power Automate整合自適應表單
description: 將自適應表單與Microsoft® Power Automet整合。
hide: true
hidefromtoc: true
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
source-git-commit: ccc4d487cb180273284276cf9cdf18680a3efcb8
workflow-type: tm+mt
source-wordcount: '1183'
ht-degree: 1%

---

# 使用Microsoft® Power Automate連接自適應表單 {#connect-adaptive-form-with-power-automate}

您可以配置自適應表單以在提交時運行Microsoft® Power自動雲流。 配置的自適應表單將捕獲的資料、附件和記錄文檔發送到Power Automate Cloud Flow進行處理。 它幫助您構建自定義資料捕獲體驗，同時利用Microsoft® Power Automate的強大功能，圍繞捕獲的資料構建業務邏輯並自動化客戶工作流。 以下是將自適應表單與Microsoft® Power Automate整合後可執行的操作的幾個示例：

* 在Power Automate業務流程中使用自適應Forms資料
* 使用Power Automate將捕獲的資料發送到500多個資料源或任何公開可用的API
* 對捕獲的資料執行複雜計算
* 按預定義的時間表將自適應Forms資料保存到儲存系統

自適應Forms編輯器提供 **調用Microsoft®電源自動流** 提交操作以發送自適應表單資料、附件和記錄文檔，並將其發送到Power Automate雲流。 要使用「提交」操作將捕獲的資料發送到Microsoft® Power Automate, [將您的Formsas a Cloud Service實例與Microsoft® Power Automate連接](forms-microsoft-power-automate-integration.md#connect-forms-server-with-power-automate)

## 必備條件

要將自適應表單與Microsoft® Power Automate連接，需要執行以下操作：

* Microsoft® Power自動化高級許可證。
* Microsoft® [電源自動流](https://docs.microsoft.com/en-us/power-automate/create-flow-solution) 和 `When an HTTP request is received` 觸發器以接受Adaptive Form submit資料。


* 具有「Forms作者」和「Forms管理」權限的Experience Manager用戶。
* 確保用於連接到Power Automate的帳戶是Power Automate流的所有者。


## 將您的Formsas a Cloud Service實例與Microsoft® Power Automate連接 {#connect-forms-server-with-power-automate}

執行以下操作以將您的Formsas a Cloud Service實例與Microsoft® Power Automate連接：

1. 建立Microsoft® Azure Active Directory應用程式
1. 建立Microsoft® Power自動化Dataverse雲配置。
1. 建立Microsoft® Power自動流式服務雲配置
1. 發佈Microsoft® Power自動化Dataverse雲配置。

### 建立Microsoft® Azure Active Directory應用程式 {#ms-power-automate-application}

1. 登錄到 [Azure門戶](https://portal.azure.com/)。
1. 選擇 [!UICONTROL Azure Active Directory] 的上界。
1. 在「預設目錄」頁上，選擇 [!UICONTROL 應用註冊] 的下界。
1. 在「應用程式註冊」頁面上，按一下「新建註冊」。
1. 在頁上指定名稱、支援的帳戶類型和重定向URI。 在重定向URI中，指定以下內容，然後按一下保存。
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![註冊Azure Active Directory應用程式](assets/power-automate-application.png)

   >[!NOTE]
   >如有必要，還可以從「驗證」頁指定其他重定向URI。
   > 對於支援的帳戶類型，根據您的使用案例選擇單個租戶、多個租戶或個人Microsoft帳戶


1. 在「驗證」頁上，啟用以下選項，然後按一下「保存」。


   * 訪問令牌（用於隱式流）
   * ID令牌（用於隱式流和混合流）

1. 在「API權限」頁上，按一下添加權限。
1. 在Microsoft® API下，選擇流服務，然後選擇以下權限。
   * Flows.Manage.All
   * Flows.Read.All

   按一下添加權限以保存權限。
1. 在「API權限」頁上，按一下添加權限。 選擇我的組織使用和搜索的API `DataVerse`。
1. 啟用user_impersonation並按一下添加權限。
1. （可選）在「證書和機密」頁面上，按一下「新建客戶機機密」。 在「添加客戶端密碼」螢幕中，提供密碼到期的說明和時間段，然後按一下「添加」。 生成秘密字串。
1. 保留特定組織的注釋 [Dynamics環境URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests)。

### 建立Microsoft® Power自動化Dataverse雲配置 {#microsoft-power-automate-dataverse-cloud-configuration}

1. 在AEM Forms作者實例上，導航到 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL 常規]** > **[!UICONTROL 配置瀏覽器]**。
1. 在 **[!UICONTROL 配置瀏覽器]** 頁面，點擊 **[!UICONTROL 建立]**。
1. 在 **[!UICONTROL 建立配置]** 對話框，指定 **[!UICONTROL 標題]** 對於配置，啟用 **[!UICONTROL 雲配置]**，然後點擊 **[!UICONTROL 建立]**。 這樣便會建立儲存 Cloud Services 的設定容器。請確保資料夾名稱未含任何空格。
1. 導航到 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power自動化Dataverse]** 並開啟在上一步中建立的配置容器。

   >[!NOTE]
   >
   >建立自適應表單時，在 **[!UICONTROL 配置容器]** 的子菜單。
1. 在配置頁上，點擊 **[!UICONTROL 建立]** 建立 [!DNL Microsoft® Power Automate Flow Service] 配置在AEM Forms。
1. 在 **[!UICONTROL 為Microsoft®電源自動化配置Dataverse服務]** ，指定 **[!UICONTROL 客戶端ID]** （也稱為應用程式ID）, **[!UICONTROL 客戶端密碼]**。 **[!UICONTROL OAuth URL]** 和 **[!UICONTROL 動態環境URL]**。 使用的客戶端ID、客戶端密鑰、OAuth URL和動態環境URL [Microsoft® Azure Active Directory應用程式](#ms-power-automate-application) 在上一節中建立。 在Microsoft® Azure Active Directory應用程式UI中使用終結點選項查找OAuth URL

![使用MicrosoftPower Automate應用程式UI中的端點選項查找OAuth URL](assets/endpoints.png)
使用Microsoft® Power自動化應用程式用戶介面中的端點選項查找OAuth URL

1. 點擊 **[!UICONTROL 連接]** 。 如有詢問，請登錄您的Microsoft® Azure帳戶。 點擊 **[!UICONTROL 保存]**。

### 建立Microsoft® Power自動流式服務雲配置。

1. 導航到 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft®電源自動流服務]** 並開啟在上一節中建立的配置容器。

   >[!NOTE]
   >
   >建立自適應表單時，在 **[!UICONTROL 配置容器]** 的子菜單。
1. 在配置頁上，點擊 **[!UICONTROL 建立]** 建立 [!DNL Microsoft® Power Automate Flow Service] 配置在AEM Forms。
1. 在 **[!UICONTROL 為Microsoft®電源自動化配置Dataverse]** ，指定 **[!UICONTROL 客戶端ID]** （也稱為應用程式ID）, **[!UICONTROL 客戶端密碼]**。 **[!UICONTROL OAuth URL]** 和 **[!UICONTROL 動態環境URL]**。 使用客戶端ID、客戶端密鑰、OAuth URL和Dynamics環境ID。 使用Microsoft® Azure Active Directory應用程式UI中的終結點選項查找OAuth URL。 開啟 [我的流](https://us.flow.microsoft.com) 連結並點擊「我的流」，使用URL中列出的ID作為Dynamics環境ID。
1. 點擊 **[!UICONTROL 連接]**。 如有詢問，請登錄您的Microsoft® Azure帳戶。 點擊 **[!UICONTROL 保存]**。

### 發佈Microsoft® Power Automate Dataverse和Microsoft® Power Automate Flow Service雲配置 {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. 導航到 **[!UICONTROL 工具]** ![錘](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Microsoft® Power自動化Dataverse]** 並開啟在上次操作中建立的配置容器 [建立Microsoft® Power自動化Dataverse雲配置](#microsoft-power-automate-dataverse-cloud-configuration) 的子菜單。
1. 選擇 `dataverse` 配置和分路 **[!UICONTROL 發佈]**。
1. 在「發佈」頁面上，選擇 **[!UICONTROL 所有配置]** 點擊 **[!UICONTROL 發佈]**。 發佈Power Automate Dataverse和Power Automate Flow Service雲配置。

您的Formsas a Cloud Service實例現在已與Microsoft® Power Automate連接。 您現在可以將自適應Forms資料發送到Power Automet流。

## 使用調用Microsoft®電源自動化流提交操作將資料發送到電源自動化流 {#use-the-invoke-microsoft-power-automate-flow-submit-action}

在你之後 [將您的Formsas a Cloud Service實例與Microsoft® Power Automate連接](#connect-forms-server-with-power-automate)，執行以下操作以配置自適應表單，以便在提交表單時將捕獲的資料發送到Microsoft®流。

1. 登錄到「作者」實例，選擇「自適應表單」，然後按一下 **[!UICONTROL 屬性]**。
1. 在「配置容器」中，瀏覽並選擇在部分中建立的容器 [建立Microsoft® Power自動化Dataverse雲配置](#microsoft-power-automate-dataverse-cloud-configuration)，然後點擊 **[!UICONTROL 保存並關閉]**。
1. 開啟自適應表單進行編輯並導航至 **[!UICONTROL 提交]** 的子目錄。
1. 在屬性容器中， **[!UICONTROL 提交操作]** 選擇 **[!UICONTROL 調用電源自動流]** 的雙曲餘切值。 可用電源自動化流清單可用 **[!UICONTROL 電源自動流]** 的雙曲餘切值。 選擇所需的流，並在提交時向其提交自適應Forms資料。

![配置提交操作](assets/submission.png)

>[!NOTE]
>
> 在提交自適應表單之前，請確保 `When an HTTP Request is received` JSON架構下的觸發器將添加到Power Automate流中。

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

