---
title: 設定 EDS Forms 的感謝頁面
description: 設定 EDS Forms 的感謝頁面
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: ht
source-wordcount: '139'
ht-degree: 100%

---


# 設定 Form 區塊重新導向

您可以選擇將 Form 區塊設定為重新導向至網站上的其他頁面，而不是預設的「感謝」頁面。將另一個頁面設定為重新導向目標

1. 開啟 `[EDS Project]/blocks/form/form.js` 檔案進行編輯。

   ![感謝節點的程式碼](/help/edge/assets/change-thankyou-node.png)

1. 將下行中的 `thankyou` 節點變更為您選擇的節點：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例如，

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'home';
   ```

   >[!NOTE]
   >
   > 確保在 Microsoft SharePoint 或 Google Sheets 的 Edge Delivery Service 專案資料夾中建立同名文件頁面 (如果尚未建立)。


1. 繼續將更新的 &#39;form.js&#39; 資料夾及其底層檔案簽入在 GitHub 的 Edge Delivery Service 專案。此更新可確保表單現在會重新導向至指定的更新節點。
