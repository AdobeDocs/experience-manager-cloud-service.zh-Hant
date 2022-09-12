---
title: 新增自訂網域名稱
description: 了解如何使用Cloud Manager新增自訂網域名稱。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 0febf4b4a59617e6cc4f8414963c4a91fcf8765e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# 新增自訂網域名稱 {#adding-cdn}

您可以在Cloud Manager的兩個位置新增自訂網域名稱：

* [從「域設定」頁](#adding-cdn-settings)
* [從環境頁面](#adding-cdn-environments)

>[!NOTE]
>
>使用者必須 **業務負責人** 或 **部署管理員** 角色，以在Cloud Manager中新增自訂網域名稱

## 從「域設定」頁添加自定義域名 {#adding-cdn-settings}

請依照下列步驟，從 **網域設定** 頁面。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **環境** 螢幕 **概述** 頁面。

1. 按一下 **網域設定** ，即可取得Advertising Cloud的說明。

   ![「域設定」窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 按一下 **添加域** 按鈕，開啟 **添加域名** 對話框。

   ![「添加域」對話框](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 在 **網域名稱** 欄位。

   >[!NOTE]
   >
   >不包括 `http://`, `https://`，或在您的網域中輸入時使用空格。

1. 選取 **環境** 其服務將與域名關聯。

1. 選取 **發佈** 或 **預覽** 服務。

1. 選取 **網域SSL憑證** 從下拉式清單中與網域名稱關聯，然後選取 **繼續**.

1. 此 **添加域名** 對話框，將帶您進入域名驗證過程。 請按照提供的說明來證明您環境的域所有權。 按一下 **建立**.

   ![域名驗證](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN部署需要有效的SSL憑證，以及成功的TXT驗證。 狀態表示 **已驗證並部署**.

請參閱檔案 [檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 進一步了解各種狀態，以及如何解決潛在問題。

>[!NOTE]
>
>由於DNS傳播延遲，DNS驗證可能需要數小時的時間才能完成。
>
>Cloud Manager會驗證所有權並更新可在網域設定表格中看到的狀態。 請參閱檔案 [檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 以取得更多詳細資訊。

>[!TIP]
>
>請參閱 [新增TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 以深入了解TXT記錄。

## 「從環境新增自訂網域名稱」頁面 {#adding-cdn-environments}

請依照下列步驟，從 **環境** 頁面。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **環境詳細資料** 興趣環境的頁面。

   ![在「環境詳細資訊」頁面上輸入域名](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用 **網域名稱** 表來提交自定義域名。

   1. 輸入自訂網域名稱。
   1. 從下拉式清單中選取與此名稱相關聯的SSL憑證。
   1. 按一下 **+添加**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 檢查 **添加域名** 對話框，按一下 **繼續**.

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >不包括 `http://`, `https://`，或在網域名稱中輸入時輸入空格。

1. 此 **添加域名** 對話框，將帶您進入域名驗證過程。 請按照提供的說明來證明您環境的域所有權。 按一下 **建立**.

   ![域名驗證](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN部署需要有效的SSL憑證，以及成功的TXT驗證。 狀態表示 **已驗證並部署**.

請參閱檔案 [檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 進一步了解各種狀態，以及如何解決潛在問題。

>[!NOTE]
>
>由於DNS傳播延遲，DNS驗證可能需要數小時的時間才能完成。
>
>Cloud Manager會驗證所有權並更新可在網域設定表格中看到的狀態。 請參閱檔案 [檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 以取得更多詳細資訊。

>[!TIP]
>
>請參閱 [新增TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 以深入了解TXT記錄。
