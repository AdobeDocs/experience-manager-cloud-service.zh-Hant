---
title: 如何為最適化Forms設定立即可用的Salesforce表單資料模型？
description: 瞭解如何整合Salesforce與最適化Forms。
feature: Adaptive Forms, Form Data Model
role: User, Developer
exl-id: 184db05b-7237-4dce-8059-03c39b93d7d7
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# 設定適用於AEM Forms的Salesforce {#configure-azure-storage}

[[!DNL Experience Manager Forms] 資料整合](data-integration.md)提供[!DNL Salesforce]雲端服務，整合最適化Forms與OOTB表單資料模型(FDM)。 最適化Forms可以與[!DNL Salesforce]伺服器互動，以啟用業務工作流程。 例如：

* 提交最適化表單時將資料寫入[!DNL Salesforce]。
* 透過表單資料模型(FDM)中定義的自訂實體將資料寫入[!DNL Salesforce]，反之亦然。
* 查詢[!DNL Salesforce]伺服器以取得資料並預先填入Adaptive Forms。
* 從[!DNL Salesforce]伺服器讀取資料。

在您[!DNL Salesforce]根據Experience Manager原型為Forms設定開發專案[!DNL AEM Forms]後，[雲端服務和表單資料模型(FDM)可在](setup-local-development-environment.md#forms-cloud-service-local-development-environment)伺服器上立即使用。

>[!NOTE]
>
>必須根據[!DNL Salesforce]AEM Archetype 30[!DNL Experience Manager Forms]或更新版本將[!DNL Cloud Service]設定為[專案，才可立即使用](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-30)雲端服務和表單資料模型(FDM)。

## 設定[!DNL Salesforce]雲端服務 {#configure-salesforce-cloud-service}

在設定[!DNL Salesforce]雲端服務之前，請確定您執行下列工作：

* [建立連線的OAuth已啟用 [!DNL Salesforce] 應用程式](https://help.salesforce.com/s/articleView?id=sf.connected_app_create_api_integration.htm&type=5)。 建立連線的[!DNL Salesforce]應用程式時，請以下列格式指定回呼URL：

  ```
  https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html
  ```

  其中伺服器和連線埠代表[!DNL AEM Forms]伺服器的主機名稱和連線埠號碼。

* 建立連線的[!DNL Salesforce]應用程式時，請指定`full`和`offline_access`做為OAuth範圍的值。

* 記下連線應用程式的使用者端ID （稱為使用者金鑰）和使用者端密碼（稱為使用者密碼）的值。

執行以下步驟來設定[!DNL Salesforce]雲端服務：

1. 在[!DNL AEM Forms]作者執行個體上，瀏覽至&#x200B;**[!UICONTROL 工具]** ![槌子](assets/hammer.png) > **[!UICONTROL 雲端服務]** > **[!UICONTROL 資料來源]**。
2. 選取資料夾名稱，選取&#x200B;**[!UICONTROL Salesforce雲端設定]**，然後選取&#x200B;**[!UICONTROL 屬性]**。
3. 在&#x200B;**[!UICONTROL 驗證設定]**&#x200B;索引標籤中：
   1. 在[!DNL Salesforce]主機&#x200B;**[!UICONTROL 欄位中指定]**&#x200B;網域URL。 例如，[網域名稱].my.salesforce.com。
   2. 為連線的應用程式指定使用者端ID （稱為使用者金鑰）和使用者端密碼（稱為使用者密碼）。
   3. 在&#x200B;**授權範圍**&#x200B;欄位中指定`full`full offline_access`offine_access` （**[!UICONTROL 和]**&#x200B;值，以空格分隔）。
   4. 選取&#x200B;**[!UICONTROL 連線至OAuth]**。 您被重新導向到[!DNL Salesforce]登入頁面。
   5. 使用您的[!DNL Salesforce]認證登入，並接受允許雲端服務設定連線到[!DNL Salesforce]服務。 如果連線成功，系統會將您重新導向至[!DNL Salesforce]雲端服務設定頁面，顯示成功訊息。
4. 選取&#x200B;**[!UICONTROL 儲存並關閉]**&#x200B;以完成組態設定。

### 存取現成可用的[!DNL Salesforce]表單資料模型(FDM)

在您[!DNL Salesforce]根據Experience Manager原型[!DNL AEM Forms]為Forms設定開發專案後，[表單資料模型(FDM)可在](setup-local-development-environment.md#forms-cloud-service-local-development-environment)伺服器上立即使用。

若要存取表單資料模型(FDM)：

1. 導覽至&#x200B;**[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 資料整合]**。
1. 選取資料夾名稱、選取&#x200B;**[!UICONTROL Salesforce資料模型]**，然後選取「編輯![編輯](assets/edit.png)」圖示以檢視表單資料模型(FDM)。

設定[[!DNL Salesforce] 雲端設定服務](#configure-salesforce-cloud-service)後，您可以將最適化表單與現成可用的[!DNL Salesforce]資料模型整合。

>[!MORELIKETHIS]
>
>* [設定AEM Forms的資料來源](/help/forms/configure-data-sources.md)
>* [設定AEM Forms的Azure儲存體](/help/forms/configure-azure-storage.md)
>  [將Forms入口網站新增至AEM Sites頁面](/help/forms/configure-forms-portal.md)
