---
title: 新增自訂網域名稱
description: 了解如何使用 Cloud Manager 新增自訂網域名稱。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 80%

---

# 新增自訂網域名稱 {#adding-cdn}

您可以從 Cloud Manager 中的兩個位置新增自訂網域名稱：

* [從域設定頁面](#adding-cdn-settings)
* [從環境頁面](#adding-cdn-environments)

>[!NOTE]
>
>使用者必須具備 **業務負責人** 或 **部署管理員** 在Cloud Manager中新增自訂網域名稱的角色

## 從域設定頁面新增自訂網域名稱 {#adding-cdn-settings}

按照以下步驟從&#x200B;**域設定**&#x200B;頁。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從「**概觀**」頁面瀏覽到「**環境**」畫面。

1. 在左側瀏覽面板中按一下&#x200B;**網域設定**。

   ![域設定窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 點擊&#x200B;**新增域**&#x200B;右上角的按鈕打開&#x200B;**新增網域名稱**&#x200B;對話。

   ![新增域對話框](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 輸入自訂網域名稱&#x200B;**網域名稱**&#x200B;場地。

   >[!NOTE]
   >
   >不包括`http://`,`https://`, 或輸入您的域時的空格。

1. 選取 **環境** 其服務與網域名稱相關聯。

1. 選擇任一&#x200B;**發布**&#x200B;或者&#x200B;**預習**&#x200B;服務。

1. 選擇&#x200B;**網域 SSL 憑證**&#x200B;從下拉清單中與網域名稱關聯並選擇&#x200B;**繼續**。

1. 這&#x200B;**新增網域名稱**&#x200B;對話框出現，將帶您進入網域名稱驗證過程。按照提供的說明證明您的環境的網域所有權。按一下&#x200B;**建立**。

   ![網域名稱識別](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN 部署需要有效的 SSL 憑證和成功的 TXT 驗證。這由狀態指示&#x200B;**驗證和部署**。

另請參閱 [檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 以進一步瞭解各種狀態以及如何解決潛在問題。

>[!NOTE]
>
>由於 DNS 傳播延遲，DNS 驗證可能需要幾個小時才能完成。
>
>Cloud Manager 將驗證所有權並更新可在域設定表中看到的狀態。另請參閱 [檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 以取得更多詳細資料。

>[!TIP]
>
>另請參閱 [新增TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 以進一步瞭解TXT記錄。

## 從環境頁面新增自訂網域名稱 {#adding-cdn-environments}

按照以下步驟從&#x200B;**環境**&#x200B;頁面。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從&#x200B;**環境**&#x200B;頁面，瀏覽到感興趣環境的詳細資訊畫面。

   ![在環境詳情頁面輸入網域名稱](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用&#x200B;**網站網域名稱**&#x200B;表提交自訂網域名稱。

   1. 輸入自訂網域名稱。
   1. 從下拉清單中選擇與此名稱關聯的 SSL 憑證。
   1. 按一下&#x200B;**「新增 +」**。

   ![新增自訂網域名稱](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 檢查在&#x200B;**新增網域名稱**&#x200B;對話框中選取的值並按一下「**繼續**」。

   ![網路名稱視窗](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >不包括`http://`,`https://`，或輸入您的網域時的空格。

1. 這&#x200B;**新增網域名稱**&#x200B;對話框出現，將帶您進入網域名稱驗證過程。按照提供的說明證明您的環境的網域所有權。按一下&#x200B;**建立**。

   ![網域名稱識別](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN 部署需要有效的 SSL 憑證和成功的 TXT 驗證。這由狀態指示&#x200B;**驗證和部署**。

另請參閱 [檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 以進一步瞭解各種狀態以及如何解決潛在問題。

>[!NOTE]
>
>由於 DNS 傳播延遲，DNS 驗證可能需要幾個小時才能完成。
>
>Cloud Manager 將驗證所有權並更新可在域設定表中看到的狀態。另請參閱 [檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 以取得更多詳細資料。

>[!TIP]
>
>另請參閱 [新增TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 以進一步瞭解TXT記錄。
