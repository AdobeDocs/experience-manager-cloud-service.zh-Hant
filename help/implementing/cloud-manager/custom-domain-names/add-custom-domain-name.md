---
title: 新增自訂網域名稱
description: 新增自訂網域名稱
translation-type: tm+mt
source-git-commit: 148a1f478aeabea970e46e7e565fccca7db6a7e9
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---


# 添加自定義域名{#adding-cdn}

用戶必須是業務擁有者或部署管理員，才能在Cloud Manager中新增自訂網域名稱。

## 重要注意事項{#important-considerations}

* 在新增自訂網域名稱之前，必須先將包含自訂網域名稱的有效SSL憑證安裝至您的程式。 請參閱[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)以瞭解詳細資訊。

* 域名無法添加到環境中，因為有一個當前正在運行的管線連接到這些環境。

* 一次只能添加一個域名。 不過，網域不能包含萬用字元。 作者端不支援自訂網域。

* 每個Cloud Manager環境最多可托管100個自定義域。

* 同一個域名不能用於多個環境。

## 從「域設定」頁{#adding-cdn-settings}添加自定義域名

請依照下列步驟，從「網域設定」頁面新增「自訂網域名稱」:

1. 從&#x200B;**概述**&#x200B;頁面導覽至&#x200B;**環境**&#x200B;畫面。

1. 從左側導覽功能表按一下「網域設定」。****

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 按一下&#x200B;**添加域**&#x200B;按鈕以開啟&#x200B;**添加域名**&#x200B;對話框。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create2.png)

1. 在&#x200B;**域名**&#x200B;中輸入自定義域名。

   >[!NOTE]
   >在您的域中輸入時，不應包括`http://`、`https://`或空格。

1. 選擇&#x200B;**Environment**，其發佈服務將與域名關聯。

1. 從下拉清單中選擇&#x200B;**域SSL證書**，然後選擇&#x200B;**繼續**。

1. **將顯示「添** 加域名稱」對話框。這將帶您進入「環境的域名驗證」螢幕。 請參閱[添加TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以瞭解詳細資訊。

   按照提供的說明來證明您環境的域所有權：

1. 按一下&#x200B;**建立**。
1. CDN部署需要有效的SSL憑證和成功的TXT驗證。 狀態&#x200B;**已驗證和已部署**表示。
導覽至[檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)，以進一步瞭解各種狀態及地址。

   >[!NOTE]
   >由於DNS傳播延遲，DNS驗證可能需要花費數小時才能識別。 Cloud Manager將驗證所有權並更新可在「網域設定表」中看到的狀態。 如需詳細資訊，請參閱檢查網域名稱狀態。

## 「從環境添加自定義域名」頁{#adding-cdn-environments}

1. 定位至感興趣環境的「環境詳細資訊」頁。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用「域名」(Domain Names)表格頂部的輸入欄位來提交自定義域名並從下拉清單中選擇SSL證書。 按一下&#x200B;**+添加**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 選中&#x200B;**添加域名**&#x200B;對話框中的欄位，然後按一下&#x200B;**繼續**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >在您的域中輸入時，請勿包含`http://`、`https://`或空格。

1. 將顯示「環境」螢幕的域名驗證。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

   請參閱[域驗證](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md)以瞭解更多資訊。 按照提供的說明來證明您環境的域所有權。

1. 按一下&#x200B;**建立**。

1. 自訂網域名稱部署需要有效的SSL憑證和成功的TXT驗證。 狀態&#x200B;**已驗證和已部署**&#x200B;表示。

此時，您的自訂網域名稱已可供測試，並有`CNAME`可供指向。 請參閱[網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)以進一步瞭解各種狀態及地址。

>[!NOTE]
>由於DNS傳播延遲，DNS驗證可能需要花費數小時才能識別。 Cloud Manager將驗證所有權並更新可在「網域設定表」中看到的狀態。 請參閱檢查域名狀態以瞭解更多資訊。
