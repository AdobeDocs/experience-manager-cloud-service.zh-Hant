---
title: 在內容傳輸工具中查看遷移集的日誌
description: 在內容傳輸工具中查看遷移集的日誌
exl-id: aed1ac83-a2fb-425e-aca4-39cd0bb42fd3
source-git-commit: 9d236e459f13fec6f0aaf80f588d20760636b9bb
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 39%

---

# 檢視移轉集記錄 {#view-logs-content-transfer-tool}


>[!CONTEXTUALHELP]
>id="aemcloud_ctt_logs"
>title="檢視記錄檔"
>abstract="提取和攝入完成後，檢查記錄檔中是否有任何錯誤/警告。如有任何錯誤應立即處理，方法是處理回報的問題或聯絡 Adobe 支援人員。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html#troubleshooting" text="疑難排解"
>additional-url="https://helpx.adobe.com/tw/enterprise/using/support-for-experience-cloud.html" text="連絡 Adobe 支援人員"

完成每個步驟（提取和攝取）後，檢查日誌並查找錯誤。  如有任何錯誤應立即處理，方法是處理回報的問題或聯絡 Adobe 支援人員。

## 查看日誌的步驟 {#viewing-logs}

### 提取日誌

要查看提取日誌，請轉到源Adobe Experience Manager實例，然後選擇所需的遷移集。

然後，執行以下步驟：

1. 選擇遷移集並按一下 **查看日誌** 按鈕。 這將顯示「日誌」對話框。 按一下 **提取日誌** 的子菜單。

   ![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam25.png) \
   或者，按一下 **已完成** 狀態：查看新頁籤中的日誌。

1. 若要追蹤記錄而不使用使用者介面，您可以透過 SSH 連線至來源 AEM 環境，並追蹤 `crx-quickstart/cloud-migration/extraction-XXXXX/output.log file`。

### 攝取日誌

要查看攝取日誌，請轉到Cloud Acceleration Manager中的攝取作業清單，然後查找所需的遷移作業並按一下三點(**...**)。 然後，可按一下 **下載日誌** 下載日誌。

![影像](/help/journey-migration/content-transfer-tool/assets-ctt/cttcam28.png)
