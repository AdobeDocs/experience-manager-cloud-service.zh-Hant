---
title: 添加自定義域名
description: 瞭解如何使用雲管理器添加自定義域名。
exl-id: 0fc427b9-560f-4f6e-ac57-32cdf09ec623
source-git-commit: 0febf4b4a59617e6cc4f8414963c4a91fcf8765e
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# 添加自定義域名 {#adding-cdn}

可以從雲管理器中的兩個位置添加自定義域名：

* [從「域設定」頁](#adding-cdn-settings)
* [從「環境」頁](#adding-cdn-environments)

>[!NOTE]
>
>用戶必須具有 **業務所有者** 或 **部署管理器** 角色，以便在Cloud Manager中添加自定義域名

## 從「域設定」頁添加自定義域名 {#adding-cdn-settings}

按照以下步驟從 **域設定** 的子菜單。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **環境** 螢幕 **概述** 的子菜單。

1. 按一下 **域設定** 的子菜單。

   ![「域設定」窗口](/help/implementing/cloud-manager/assets/cdn/cdn-create.png)

1. 按一下 **添加域** 按鈕 **添加域名** 對話框。

   ![「添加域」對話框](/help/implementing/cloud-manager/assets/cdn/add-cdn1.png)

1. 在 **域名** 的子菜單。

   >[!NOTE]
   >
   >不包括 `http://`。 `https://`或空格。

1. 選擇 **環境** 其服務將與域名關聯。

1. 選擇 **發佈** 或 **預覽** 服務。

1. 選擇 **域SSL證書** 與下拉清單中的域名關聯，然後選擇 **繼續**。

1. 的 **添加域名** 對話框，並將帶您進入域名驗證過程。 按照提供的說明來證明您環境的域所有權。 按一下 **建立**。

   ![域名驗證](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN部署需要有效的SSL證書和成功的TXT驗證。 這由狀態指示 **已驗證並部署**。

請參閱文檔 [正在檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 瞭解有關各種狀態以及如何解決潛在問題的更多資訊。

>[!NOTE]
>
>由於DNS傳播延遲，DNS驗證可能需要幾個小時才能完成。
>
>雲管理器將驗證所有權並更新可在「域設定」表中看到的狀態。 請參閱文檔 [正在檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 的子菜單。

>[!TIP]
>
>請參閱 [添加TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 瞭解有關TXT記錄的詳細資訊。

## 「從環境添加自定義域名」頁 {#adding-cdn-environments}

按照以下步驟從 **環境** 的子菜單。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **環境詳細資訊** 的子菜單。

   ![在「環境詳細資料」頁上輸入域名](/help/implementing/cloud-manager/assets/cdn/cdn-create4.png)

1. 使用 **域名** 表以提交自定義域名。

   1. 輸入自定義域名。
   1. 從下拉清單中選擇與此名稱關聯的SSL證書。
   1. 按一下 **+添加**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create3.png)

1. 檢查在 **添加域名** 對話框，按一下 **繼續**。

   ![](/help/implementing/cloud-manager/assets/cdn/cdn-create5.png)

   >[!NOTE]
   >
   >不包括 `http://`。 `https://`，或輸入域名時使用空格。

1. 的 **添加域名** 對話框，並將帶您進入域名驗證過程。 按照提供的說明來證明您環境的域所有權。 按一下 **建立**。

   ![域名驗證](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

CDN部署需要有效的SSL證書和成功的TXT驗證。 這由狀態指示 **已驗證並部署**。

請參閱文檔 [正在檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 瞭解有關各種狀態以及如何解決潛在問題的更多資訊。

>[!NOTE]
>
>由於DNS傳播延遲，DNS驗證可能需要幾個小時才能完成。
>
>雲管理器將驗證所有權並更新可在「域設定」表中看到的狀態。 請參閱文檔 [正在檢查自定義域名狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) 的子菜單。

>[!TIP]
>
>請參閱 [添加TXT記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) 瞭解有關TXT記錄的詳細資訊。
