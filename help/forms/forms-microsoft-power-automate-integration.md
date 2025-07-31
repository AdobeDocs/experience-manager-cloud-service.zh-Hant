---
title: 如何將最適化表單與Microsoft&amp； reg； Power Automate整合？
description: 整合最適化表單與Microsoft&amp； reg； Power Automate。
exl-id: a059627b-df12-454d-9e2c-cc56986b7de6
keywords: 將AEM表單連線至power automate、Power automate automation AEM Forms、將power automate整合至Adaptive Forms、將資料從Adaptive Forms傳送至Power Automate
feature: Adaptive Forms, Foundation Components, Core Components, Edge Delivery Services
role: Admin, User, Developer
source-git-commit: c0df3c6eaf4e3530cca04157e1a5810ebf5b4055
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 11%

---


# 連線最適化表單與Microsoft® Power Automate {#connect-adaptive-form-with-power-automate}

<span class="preview">如果您使用GovCloud且需要連線至GCC （政府雲端運算）租使用者，請從您的官方地址傳送電子郵件至aem-forms-ea@adobe.com，以透過早期採用者計畫請求存取權。</span>

您可以設定最適化表單，在提交時執行 Microsoft® Power Automate Cloud Flow。設定的最適化表單會將擷取的資料、附件和記錄文件傳送到 Power Automate Cloud Flow 進行處理。它可幫助您建立自訂資料擷取體驗，同時利用Microsoft® Power Automate的強大功能，圍繞擷取的資料建立商業邏輯，並自動化客戶工作流程。

最適化Forms編輯器提供&#x200B;**叫用Microsoft®Power Automate流程**&#x200B;提交動作，以將最適化表單資料、附件和記錄檔案傳送至Power Automate雲端流程。

AEM as a Cloud Service提供多種立即可用的提交動作，用於處理表單提交。 您可以在[最適化表單提交動作](/help/forms/aem-forms-submit-action.md)文章中進一步瞭解這些選項。


## 優點

以下是整合最適化表單與 Microsoft® Power Automate 後，可以執行的部分操作範例：

* 在 Power Automate 業務流程中使用最適化表單資料
* 使用 Power Automate 將擷取的資料傳送到 500 多個資料來源或任何公開可用的 API
* 對擷取的資料執行複雜的計算
* 按預定義的排程將最適化表單資料儲存到儲存系統

## 先決條件

以下為連線最適化表單與Microsoft® Power Automate的必要條件：

* Microsoft® Power Automate Premium授權。
* Microsoft® [具有](https://docs.microsoft.com/en-us/power-automate/create-flow-solution)觸發程式的Power Automate流程`When an HTTP request is received`以接受最適化表單提交資料。
* 具有[Forms作者](/help/forms/forms-groups-privileges-tasks.md)和[Forms管理員](/help/forms/forms-groups-privileges-tasks.md)許可權的Experience Manager使用者
* 用來連線至Microsoft的帳戶®Power Automate是已設定為可從調適型表單接收資料的Power Automate流程的所有者

## 將Forms as a Cloud Service執行個體與Microsoft® Power Automate連線 {#connect-forms-server-with-power-automate}

執行以下動作，將您的Forms as a Cloud Service執行個體與Microsoft® Power Automate連線：

1. [建立Microsoft](#ms-power-automate-application)
1. [建立Microsoft](#microsoft-power-automate-dataverse-cloud-configuration)
1. [建立Microsoft](#create-microsoft-power-automate-flow-cloud-configuration)
1. [發佈Microsoft](#publish-microsoft-power-automate-dataverse-cloud-configuration)

### 建立Microsoft® Azure Active Directory應用程式 {#ms-power-automate-application}

1. 登入[Azure入口網站](https://portal.azure.com/)。
1. 從左側導覽中選取[!UICONTROL Azure Active Directory]。
1. 在預設目錄頁面上，從左側面板選取[!UICONTROL 應用程式註冊]。
1. 在「應用程式註冊」頁面上，按一下「新註冊」 。
1. 在頁面上指定名稱、支援的帳戶型別和重新導向URI。 在「重新導向URI」中，指定下列專案，然後按一下「儲存」。
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/dataverse/config.html`
   * `https://[Forms as a Cloud Service Server]/libs/fd/powerautomate/content/flowservice/config.html`

   ![註冊Azure Active Directory應用程式](assets/power-automate-application.png)

   >[!NOTE]
   >如有需要，您也可以從「驗證」頁面指定其他重新導向URI。
   > 對於支援的帳戶型別，請根據您的使用案例選取單一租使用者、多個租使用者或個人Microsoft®帳戶


1. 在「驗證」頁面上，啟用下列選項，然後按一下「儲存」。


   * 存取權杖（用於隱含流程）
   * ID權杖（用於隱含和混合流量）

1. 在API許可權頁面上按一下`Add a permission`。

1. 在Microsoft® API底下，選取`Power Automate`，然後選取下列許可權。
   * Flows.Manage.All
   * Flows.Read.All
   * GCC許可權(如果您想要連線至GCC （政府雲端運算）租使用者，則為選用)
按一下`Add permissions`以儲存許可權。
1. 在API許可權頁面上按一下`Add a permission`。 選取我的組織使用的API並搜尋`DataVerse`和啟用`user_impersonation`按一下`Add`許可權。
1. （選擇性）在「憑證和密碼」頁面上，按一下「新增使用者端密碼」。 在「新增使用者端密碼」畫面上，提供密碼到期的說明和時段，然後按一下「新增」。 產生秘密字串。
1. 記下貴組織專屬的[動態環境URL](https://docs.microsoft.com/en-us/power-automate/web-api#compose-http-requests)。

### 建立Microsoft® Power Automate Dataverse雲端設定 {#microsoft-power-automate-dataverse-cloud-configuration}

1. 在AEM Forms作者執行個體上，瀏覽至&#x200B;**[!UICONTROL 工具]** ![hammer](assets/hammer.png) > **[!UICONTROL 一般]** > **[!UICONTROL 設定瀏覽器]**。
1. 在&#x200B;**[!UICONTROL 設定瀏覽器]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 建立]**。
1. 在&#x200B;**[!UICONTROL 建立設定]**&#x200B;對話方塊中，指定設定的&#x200B;**[!UICONTROL 標題]**、啟用&#x200B;**[!UICONTROL 雲端設定]**，並選取&#x200B;**[!UICONTROL 建立]**。 這樣便會建立儲存 Cloud Services 的設定容器。請確保資料夾名稱未含任何空格。
1. 瀏覽至&#x200B;**[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL Microsoft® Power Automate Dataverse]**，並開啟您在上一步中建立的設定容器。


   >[!NOTE]
   >
   >建立最適化表單時，請在&#x200B;**[!UICONTROL 設定容器]**&#x200B;欄位中指定容器名稱。

1. 在設定頁面上，選取「**[!UICONTROL 建立]**」以在AEM Forms中建立[!DNL Microsoft® Power Automate Flow Service]設定。
1. 在&#x200B;**[!UICONTROL 設定Microsoft® Power Automate的Dataverse服務]**&#x200B;頁面上，指定&#x200B;**[!UICONTROL 使用者端ID]** （也稱為應用程式ID）、**[!UICONTROL 使用者端密碼]**、**[!UICONTROL OAuth URL]**&#x200B;和&#x200B;**[!UICONTROL 動態環境URL]**。 使用您在上一節建立的[Microsoft® Azure Active Directory應用程式](#ms-power-automate-application)的使用者端ID、使用者端密碼、OAuth URL和動態環境URL。 在Microsoft® Azure Active Directory應用程式UI中使用端點選項來尋找OAuth URL

   ![在Microsoft Power Automate應用程式UI中使用端點選項來尋找OAuth URL](assets/endpoints.png)

1. 選取&#x200B;**[!UICONTROL 連線]** 。 如有要求，請登入您的Microsoft® Azure帳戶。 選取「**[!UICONTROL 儲存]**」。

### 建立Microsoft® Power Automate流程服務雲端設定 {#create-microsoft-power-automate-flow-cloud-configuration}

1. 瀏覽至&#x200B;**[!UICONTROL 工具]** ![hammer](assets/hammer.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL Microsoft® Power Automate流程服務]**，並開啟您在上一節中建立的設定容器。


   >[!NOTE]
   >
   >建立最適化表單時，請在&#x200B;**[!UICONTROL 設定容器]**&#x200B;欄位中指定容器名稱。

1. 在設定頁面上，選取「**[!UICONTROL 建立]**」以在AEM Forms中建立[!DNL Microsoft® Power Automate Flow Service]設定。

1. （選擇性）選取`Connect to Microsoft GCC`核取方塊以連線至GCC租使用者。

   >[!NOTE]
   >
   > 如果您想要連線到GCC （政府雲端運算）租使用者，請在Microsoft Azure入口網站中選取GCC許可權。


   ![Power Automate雲端設定](/help/forms/assets/power-automate.png)

1. 在&#x200B;**[!UICONTROL 設定Microsoft® Power Automate的Dataverse]**&#x200B;頁面上，指定&#x200B;**[!UICONTROL 使用者端ID]** （也稱為應用程式ID）、**[!UICONTROL 使用者端密碼]**、**[!UICONTROL OAuth URL]**&#x200B;和&#x200B;**[!UICONTROL 動態環境URL]**。 使用使用者端ID、使用者端密碼、OAuth URL和Dynamics環境ID。 在Microsoft® Azure Active Directory應用程式UI中使用端點選項來尋找OAuth URL。 開啟[我的資料流](https://us.flow.microsoft.com)連結，然後選取「我的資料流」使用URL中列出的識別碼做為Dynamics環境ID。

1. 選取&#x200B;**[!UICONTROL 連線]**。 如有要求，請登入您的Microsoft® Azure帳戶。 選取「**[!UICONTROL 儲存]**」。

### 發佈Microsoft® Power Automate Dataverse和Microsoft® Power Automate流程服務雲端設定 {#publish-microsoft-power-automate-dataverse-cloud-configuration}

1. 瀏覽至&#x200B;**[!UICONTROL 工具]** ![hammer](assets/hammer.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL Microsoft® Power Automate Dataverse]**，並開啟您在上一個[建立Microsoft® Power Automate Dataverse雲端設定](#microsoft-power-automate-dataverse-cloud-configuration)區段中建立的設定容器。
1. 選取`dataverse`組態並選取&#x200B;**[!UICONTROL 發佈]**。
1. 在發佈頁面上，選取&#x200B;**[!UICONTROL 所有組態]**&#x200B;並選取&#x200B;**[!UICONTROL 發佈]**。 發佈Power Automate Dataverse和Power Automate流程服務雲端設定。

您的Forms as a Cloud Service執行個體現在已與Microsoft® Power Automate連線。 您現在可以將最適化Forms資料傳送到Power Automate流程。

## 使用叫用Microsoft® Power Automate流程提交動作將資料傳送至Power Automate流程 {#use-the-invoke-microsoft-power-automate-flow-submit-action}

在您[將您的Forms as a Cloud Service執行個體與Microsoft® Power Automate](#connect-forms-server-with-power-automate)連線後，執行以下動作來設定您的最適化表單，以在表單提交時將擷取的資料傳送到Microsoft®流程。

>[!BEGINTABS]

>[!TAB 基礎元件]

1. 登入您的Author執行個體，選取您的Adaptive Form並按一下&#x200B;**[!UICONTROL 屬性]**。
1. 在設定容器中，瀏覽並選取在[建立Microsoft® Power Automate Dataverse雲端設定](#microsoft-power-automate-dataverse-cloud-configuration)區段中建立的容器，並選取&#x200B;**[!UICONTROL 儲存並關閉]**。
1. 開啟最適化表單以進行編輯，並導覽至最適化表單容器屬性的&#x200B;**[!UICONTROL 提交]**&#x200B;區段。
1. 在屬性容器中，針對&#x200B;**[!UICONTROL 提交動作]**，選取&#x200B;**[!UICONTROL 叫用Power Automate流程]**&#x200B;選項，並選取&#x200B;**[!UICONTROL Power Automate流程]**。 選取所需的流程，並在提交時提交最適化Forms資料。

   ![設定提交動作](assets/submission.png)
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!NOTE]
>
> 在提交最適化表單之前，請確定已將具有以下JSON結構描述的`When an HTTP Request is received`觸發器新增到您的Power Automate流程。

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

>[!TAB 核心元件]

1. 登入您的Author執行個體，選取您的Adaptive Form並按一下&#x200B;**[!UICONTROL 屬性]**。
1. 在設定容器中，瀏覽並選取在[建立Microsoft® Power Automate Dataverse雲端設定](#microsoft-power-automate-dataverse-cloud-configuration)區段中建立的容器，並選取&#x200B;**[!UICONTROL 儲存並關閉]**。
1. 開啟內容瀏覽器，然後選取最適化表單的「**[!UICONTROL 指引容器]**」元件。
1. 按一下「指引容器」屬性 ![指引屬性](/help/forms/assets/configure-icon.svg) 圖示。此時會開啟「最適化表單容器」對話框。
1. 按一下「**[!UICONTROL 提交]**」標籤。
1. 從[提交]動作下拉式清單中選取&#x200B;**[!UICONTROL 叫用Power Automate流程]**&#x200B;選項，然後選取&#x200B;**[!UICONTROL Power Automate流程]**。 選取所需的流程，並在提交時提交最適化Forms資料。

   ![設定提交動作](/help/forms/assets/power-automate-cc.png)
1. 按一下&#x200B;**[!UICONTROL 「完成」]**。

>[!NOTE]
>
> 在提交最適化表單之前，請確定已將具有以下JSON結構描述的`When an HTTP Request is received`觸發器新增到您的Power Automate流程。

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

>[!TAB 通用編輯器]

1. 登入您的Author例項，選取您的Adaptive Form。
1. 在設定容器中，瀏覽並選取在[建立Microsoft® Power Automate Dataverse雲端設定](#microsoft-power-automate-dataverse-cloud-configuration)區段中建立的容器，並選取&#x200B;**[!UICONTROL 儲存並關閉]**。
1. 開啟最適化表單進行編輯。
1. 按一下編輯器上的&#x200B;**編輯表單屬性**&#x200B;擴充功能。
**表單屬性**&#x200B;對話方塊就會顯示。

   >[!NOTE]
   >
   > * 如果您在通用編輯器介面中看不到&#x200B;**編輯表單屬性**&#x200B;圖示，請在Extension Manager中啟用&#x200B;**編輯表單屬性**&#x200B;擴充功能。
   > * 請參閱[Extension Manager功能焦點](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)文章，瞭解如何在通用編輯器中啟用或停用擴充功能。


1. 按一下&#x200B;**提交**&#x200B;索引標籤，然後選取&#x200B;**[!UICONTROL 叫用Power Automate流程]**&#x200B;提交動作。 選取所需的流程，並在提交時提交最適化Forms資料。

   ![設定提交動作](/help/forms/assets/power-automate-ue.png)
1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。

>[!NOTE]
>
> 在提交最適化表單之前，請確定已將具有以下JSON結構描述的`When an HTTP Request is received`觸發器新增到您的Power Automate流程。

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

>[!ENDTABS]

<!--
## See also

* [Create an Adaptive Form](creating-adaptive-form-core-components.md)
* [Configure a Submit Action](configure-submit-actions-core-components.md)
* [Adobe Experience Manager Connector for Microsoft&reg; Power Automate](https://learn.microsoft.com/en-us/connectors/adobeexperiencemanag/)
* [Connect Adaptive Form to Microsoft&reg; Power Automate](/help/forms/configure-submit-actions-core-components.md#microsoft-power-automate)
-->


## 相關文章

{{af-submit-action}}

<!--

>[!MORELIKETHIS]
>
>* [Connect Adaptive Form to Microsoft Power Automate](/help/forms/configure-submit-actions-core-components.md#microsoft-power-automate)

-->