---
title: 添加自定義域名
description: 添加自定義域名
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 98c137645351c86da8680a31b4929c588863a981
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# 添加自定義域名 {#adding-cdn}

用戶必須是業務所有者或部署管理器，才能在雲管理器中添加自定義域名。

必須按下表所示完成以下步驟：

| 步驟 |  | 責任 | 了解更多 |
|--- |--- |--- |---|
| 添加SLL證書 | 添加SLL證書 | 客戶 | [添加SSL證書](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| 域驗證 | 添加TXT記錄 | 客戶 | [添加TXT記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| 查看域驗證狀態 |  | 客戶 |  |
|  | 狀態：域驗證失敗 | 客戶 | [正在檢查域名狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | 狀態：已驗證，部署失敗 | 聯繫Adobe代表 | [正在檢查域名狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| 通過添加CNAME或APEX記AEM錄添加指向as a Cloud Service的DNS記錄 | 配置DNS設定 | 客戶 | [配置DNS設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| 檢查DNS記錄狀態 |  | 客戶 | [正在檢查DNS記錄狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 狀態：未檢測到DNS狀態 | 客戶 | [正在檢查DNS記錄狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 狀態：DNS解析不正確 | 客戶 |  |


## 重要注意事項 {#important-considerations}

* 在添加自定義域名之前，必須將包含自定義域名的有效SSL證書安裝到您的程式中。 請參閱 [添加SSL證書](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) 來瞭解更多資訊。

* 當有當前正在運行的管道連接到這些環境時，無法將域名添加到這些環境。

* 一次只能添加一個域名。 不支援作者端的自定義域。

* AEMas a Cloud Service不支援通配符域。

* 每個Cloud Manager環境最多可承載每個環境500個自定義域。

* 同一域名不能用於多個環境。

## 從「域設定」頁添加自定義域名 {#adding-cdn-settings}

按照以下步驟從「域設定」頁添加「自定義域名」：

1. 導航到 **環境** 螢幕 **概述** 的子菜單。

1. 按一下 **域設定** 的下界。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 按一下 **添加域** 按鈕開啟 **添加域名** 對話框。

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 在中輸入自定義域名 **域名**。

   >[!NOTE]
   >您不應包括 `http://`。 `https://`或空格。

1. 選擇 **環境** 其發佈服務將與域名關聯。

1. 選擇服務作為 **發佈** 或 **預覽**。

   >[!NOTE]
   >現在，發佈服務和預覽服務的Cloud Manager for Sites程式支援自定義域名。 每個Cloud Manager環境最多可承載每個環境500個自定義域。 要瞭解有關預覽服務的詳細資訊，請參閱 [預覽服務](/help/implementing/cloud-manager/manage-environments.md#preview-service)。

1. 選擇 **域SSL證書** 從下拉框中選擇 **繼續**。

1. **添加域名** 對話框。 這將帶您進入「環境的域名驗證」螢幕。 請參閱 [添加TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 來瞭解更多資訊。

   按照提供的說明來證明您環境的域所有權：

1. 按一下 **建立**。
1. CDN部署需要有效的SSL證書和成功的TXT驗證。 這由狀態指示 **已驗證並部署**。
導航到 [正在檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 瞭解有關各種狀態以及如何解決的詳細資訊。

   >[!NOTE]
   >由於DNS傳播延遲，DNS證明可能需要幾個小時才能識別。 雲管理器將驗證所有權並更新可在「域設定」表中看到的狀態。 有關詳細資訊，請參閱檢查域名狀態。

## 「從環境添加自定義域名」頁 {#adding-cdn-environments}

1. 定位至所關注環境的「環境詳細資訊」頁。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用「域名」(Domain Names)表格頂部的輸入欄位提交自定義域名，然後從下拉清單中選擇SSL證書。 按一下 **+添加**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 檢查 **添加域名** 對話框，按一下 **繼續**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >不包括 `http://`。 `https://`或空格。

1. 將顯示「Domain Name Verification for your Environment（環境的域名驗證）」螢幕。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   請參閱 [域驗證](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 來瞭解更多資訊。 按照提供的說明來證明您環境的域所有權。

1. 按一下 **建立**。

1. 自定義域名部署需要有效的SSL證書和成功的TXT驗證。 這由狀態指示 **已驗證並部署**。

此時，您的自定義域名已準備好進行測試，並且 `CNAME` 指向它。 請參閱 [域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 瞭解有關各種狀態以及如何解決的詳細資訊。

>[!NOTE]
>由於DNS傳播延遲，DNS證明可能需要幾個小時才能識別。 雲管理器將驗證所有權並更新可在「域設定」表中看到的狀態。 請參閱檢查域名狀態以瞭解更多資訊。
