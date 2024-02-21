---
title: 為EDS Forms設定感謝頁面
description: 為EDS Forms設定感謝頁面
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 0604838311bb9ab195789fad755b0910e09519fd
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 5%

---


# 設定表單區塊重新導向

您可以選擇將表單區塊設定為重新導向至您網站上的不同頁面，而不是預設的「感謝您」頁面。 若要將其他頁面設定為重新導向目的地

1. 閇啟 `[EDS Project]/blocks/form/form.js` 檔案進行編輯。

   ![感謝節點的程式碼](/help/edge/assets/change-thankyou-node.png)

1. 變更 `thankyou` 節點至您選擇的節點：

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'thankyou';
   ```

   例如，

   ```JavaScript
   window.location.href = form.dataset?.redirect || 'home';
   ```

   >[!NOTE]
   >
   > 請確認已在Microsoft SharePoint或Google Sheets上的Edge Delivery Service專案資料夾中建立同名檔案頁面（如果尚未建立）。


1. 繼續將更新的「form.js」資料夾及其基礎檔案簽入GitHub上的Edge Delivery Service專案。 此更新可確保表單現在會依指定重新導向至更新的節點。
