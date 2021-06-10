---
title: 新增自訂網域名稱
description: 新增自訂網域名稱
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 1eb9423b0128c952bc16cf0b8dff95b0e86964a0
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# 添加自定義域名{#adding-cdn}

使用者必須是業務擁有者或部署管理員，才能在Cloud Manager中新增自訂網域名稱。

## 重要注意事項{#important-considerations}

* 添加自定義域名之前，必須先將包含自定義域名的有效SSL證書安裝到您的程式中。 請參閱[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)以深入了解。

* 當有一個當前正在運行的管道連接到這些環境時，無法將域名添加到環境中。

* 一次只能添加一個域名。 不過，網域不能包含萬用字元。 不支援製作端的自訂網域。

* AEM as aCloud Service不支援萬用字元網域。

* 每個Cloud Manager環境最多可托管每個環境250個自訂網域。

* 同一個域名不能用於多個環境。

## 從「域設定」頁{#adding-cdn-settings}添加自定義域名

請依照下列步驟，從「網域設定」頁面新增「自訂網域名稱」 :

1. 從&#x200B;**概述**&#x200B;頁面導覽至&#x200B;**環境**&#x200B;畫面。

1. 按一下左側導航菜單中的&#x200B;**域設定**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 按一下&#x200B;**添加域**&#x200B;按鈕以開啟&#x200B;**添加域名**&#x200B;對話框。

   ![](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 在&#x200B;**域名**&#x200B;中輸入自定義域名。

   >[!NOTE]
   >在域中輸入時，不應包含`http://`、`https://`或空格。

1. 選擇其發佈服務將與域名關聯的&#x200B;**環境**。

1. 選擇服務作為&#x200B;**Publish**&#x200B;或&#x200B;**Preview**。

   >[!NOTE]
   >Cloud Manager現在支援自訂網域名稱，適用於發佈和預覽服務的Sites程式。 每個Cloud Manager環境最多可托管每個環境250個自訂網域。 若要深入了解預覽服務，請參閱[預覽服務](/help/implementing/cloud-manager/manage-environments.md#preview-service)。

1. 從下拉式清單中選取&#x200B;**網域SSL憑證**，然後選取&#x200B;**繼續**。

1. **「Add Domain(添加** 域)」對話框出現。這會將您帶到「環境的域名驗證」螢幕。 請參閱[新增TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以深入了解。

   按照提供的說明證明您環境的域所有權：

1. 按一下&#x200B;**Create**。
1. CDN部署需要有效的SSL憑證，以及成功的TXT驗證。 狀態&#x200B;**已驗證且已部署**表示。
導覽至「[檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 」，深入了解各種狀態及處理方式。

   >[!NOTE]
   >由於DNS傳播延遲，DNS校樣可能需要數小時才能識別。 Cloud Manager會驗證所有權並更新可在網域設定表格中看到的狀態。 如需詳細資訊，請參閱檢查網域名稱狀態。

## 從環境頁面{#adding-cdn-environments}新增自訂網域名稱

1. 導覽至感興趣環境的環境詳細資料頁面。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用「域名」(Domain Names)表格頂部的輸入欄位來提交自定義域名，並從下拉清單中選擇SSL證書。 按一下&#x200B;**+ Add**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 檢查&#x200B;**添加域名**&#x200B;對話框中的欄位，然後按一下&#x200B;**繼續**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >在網域中輸入時，請勿包含`http://`、`https://`或空格。

1. 「環境的域名驗證」螢幕隨即顯示。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   請參閱[網域驗證](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以深入了解。 請按照提供的說明來證明您環境的域所有權。

1. 按一下&#x200B;**Create**。

1. 自訂網域名稱部署需要有效的SSL憑證，並且需要成功的TXT驗證。 狀態&#x200B;**已驗證且已部署**&#x200B;表示。

此時，您的自訂網域名稱已準備好進行測試，且`CNAME`會指向它。 請參閱[網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)以進一步了解各種狀態及如何處理。

>[!NOTE]
>由於DNS傳播延遲，DNS校樣可能需要數小時才能識別。 Cloud Manager會驗證所有權並更新可在網域設定表格中看到的狀態。 如需詳細資訊，請參閱檢查網域名稱狀態。
