---
title: 新增自訂網域名稱
description: 新增自訂網域名稱
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 98c137645351c86da8680a31b4929c588863a981
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# 新增自訂網域名稱 {#adding-cdn}

使用者必須是業務擁有者或部署管理員，才能在Cloud Manager中新增自訂網域名稱。

必須依照下表所述完成下列步驟：

| 步驟 |  | 責任 | 了解更多 |
|--- |--- |--- |---|
| 添加SLL證書 | 添加SLL證書 | 客戶 | [新增SSL憑證](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| 域驗證 | 新增TXT記錄 | 客戶 | [新增TXT記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| 查看域驗證狀態 |  | 客戶 |  |
|  | 狀態：域驗證失敗 | 客戶 | [檢查域名狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | 狀態：已驗證，部署失敗 | 聯絡Adobe代表 | [檢查域名狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| 新增CNAME或APEX記錄，以新增指向AEMas a Cloud Service的DNS記錄 | 配置DNS設定 | 客戶 | [配置DNS設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| 檢查DNS記錄狀態 |  | 客戶 | [正在檢查DNS記錄狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 狀態：未檢測到DNS狀態 | 客戶 | [正在檢查DNS記錄狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 狀態：DNS解析不正確 | 客戶 |  |


## 重要考量 {#important-considerations}

* 添加自定義域名之前，必須先將包含自定義域名的有效SSL證書安裝到您的程式中。 請參閱 [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 了解更多。

* 當有一個當前正在運行的管道連接到這些環境時，無法將域名添加到環境中。

* 一次只能添加一個域名。 不支援製作端的自訂網域。

* AEMas a Cloud Service不支援萬用字元網域。

* 每個Cloud Manager環境最多可托管每個環境500個自訂網域。

* 同一個域名不能用於多個環境。

## 從「域設定」頁添加自定義域名 {#adding-cdn-settings}

請依照下列步驟，從「網域設定」頁面新增「自訂網域名稱」 :

1. 導覽至 **環境** 螢幕 **概述** 頁面。

1. 按一下 **網域設定** 的上界。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 按一下 **添加域** 按鈕 **添加域名** 對話框。

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 在 **網域名稱**.

   >[!NOTE]
   >您不應包含 `http://`, `https://`，或在您的網域中輸入時使用空格。

1. 選取 **環境** 其發佈服務將與網域名稱相關聯。

1. 選擇服務作為 **發佈** 或 **預覽**.

   >[!NOTE]
   >Cloud Manager現在支援自訂網域名稱，適用於發佈和預覽服務的Sites程式。 每個Cloud Manager環境最多可托管每個環境500個自訂網域。 若要進一步了解預覽服務，請參閱 [預覽服務](/help/implementing/cloud-manager/manage-environments.md#preview-service).

1. 選取 **網域SSL憑證** 從下拉式清單中選取 **繼續**.

1. **添加域名** 對話框。 這會將您帶到「環境的域名驗證」螢幕。 請參閱 [新增TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 了解更多。

   按照提供的說明證明您環境的域所有權：

1. 按一下 **建立**.
1. CDN部署需要有效的SSL憑證，以及成功的TXT驗證。 狀態表示 **已驗證並部署**.
導覽至 [檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 以進一步了解各種狀態及處理方式。

   >[!NOTE]
   >由於DNS傳播延遲，DNS校樣可能需要數小時才能識別。 Cloud Manager會驗證所有權並更新可在網域設定表格中看到的狀態。 如需詳細資訊，請參閱檢查網域名稱狀態。

## 「從環境新增自訂網域名稱」頁面 {#adding-cdn-environments}

1. 導覽至感興趣環境的環境詳細資料頁面。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用「域名」(Domain Names)表格頂部的輸入欄位來提交自定義域名，並從下拉清單中選擇SSL證書。 按一下 **+新增**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 檢查 **添加域名** 對話框，按一下 **繼續**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >不包括 `http://`, `https://`，或在您的網域中輸入時使用空格。

1. 「環境的域名驗證」螢幕隨即顯示。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   請參閱 [域驗證](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 了解更多。 請按照提供的說明來證明您環境的域所有權。

1. 按一下 **建立**.

1. 自訂網域名稱部署需要有效的SSL憑證，並且需要成功的TXT驗證。 狀態表示 **已驗證並部署**.

此時，您的自訂網域名稱已可供測試，且 `CNAME` 指向它。 請參閱 [域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 以進一步了解各種狀態及處理方式。

>[!NOTE]
>由於DNS傳播延遲，DNS校樣可能需要數小時才能識別。 Cloud Manager會驗證所有權並更新可在網域設定表格中看到的狀態。 如需詳細資訊，請參閱檢查網域名稱狀態。
