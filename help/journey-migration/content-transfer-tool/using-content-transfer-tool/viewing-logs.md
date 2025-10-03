---
title: 在內容轉移工具中檢視移轉集記錄
description: 在內容轉移工具中檢視移轉集記錄
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
feature: Migration
role: Admin
source-git-commit: 91f9bcafc087b6f9329d7a47509cc659714705ff
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 36%

---

# 檢視移轉集記錄 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="檢視記錄檔"
>abstract="提取和攝入完成後，檢查記錄檔中是否有任何錯誤/警告。如有任何錯誤應立即處理，方法是處理回報的問題或聯絡 Adobe 支援人員。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=zh-Hant#troubleshooting" text="疑難排解"
>additional-url="https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html" text="連絡 Adobe 支援人員"

完成每個步驟（擷取和擷取）後，請檢查記錄檔並尋找錯誤。  如有任何錯誤應立即處理，方法是處理回報的問題或聯絡 Adobe 支援人員。

## 檢視記錄的步驟 {#viewing-logs}

### 擷取記錄

若要檢視擷取記錄，請前往您的來源Adobe Experience Manager執行個體，然後選取所需的移轉集。

接著，請遵循下列步驟：

1. 選取移轉集，然後按一下動作列中的&#x200B;**檢視記錄檔**。 這會顯示「記錄」對話方塊。 按一下&#x200B;**擷取記錄**，在新索引標籤中檢視記錄。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/logs.png) \
   或者，按一下&#x200B;**已完成**&#x200B;狀態以在新索引標籤中檢視記錄。

1. 若要追蹤記錄而不使用使用者介面，您可以透過 SSH 連線至來源 AEM 環境，並追蹤 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。

### 內嵌記錄

若要檢視內嵌記錄，請前往Cloud Acceleration Manager中的內嵌工作清單，然後尋找所需的移轉工作，並按一下工作的三個點(**...**)。 然後，您可以按一下&#x200B;**下載記錄檔**&#x200B;來下載記錄檔。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
