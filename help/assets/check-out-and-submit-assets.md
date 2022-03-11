---
title: 簽入和簽出檔案 [!DNL Assets]
description: 瞭解如何簽出資產以進行編輯，並在更改完成後將其簽回。
contentOwner: AG
feature: Asset Management
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: 034899c2a717fafdc50cc269d6db3feb77d907c5
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# 簽入和簽出檔案 [!DNL Experience Manager] 水壩 {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] 允許您簽出要編輯的資產，並在完成更改後將其簽回。 簽出資產後，只有您才能編輯、注釋、發佈、移動或刪除資產。 簽出資產會鎖定資產。 在您將資產簽回至 [!DNL Assets]。 但是，他們仍然可以更改鎖定資產的元資料。

要能夠簽出/簽入資產，您需要對其進行寫入訪問。

此功能有助於防止其他用戶覆蓋作者所做的更改，其中多個用戶在跨團隊編輯工作流時進行協作。

## 簽出資產 {#checking-out-assets}

1. 從 [!DNL Assets] 用戶介面，選擇要簽出的資產。 您也可以選擇多個資產以簽出。

1. 在工具欄中，按一下 **[!UICONTROL 簽出]**。 的 **[!UICONTROL 簽出]** 選項切換至 **[!UICONTROL 簽入]**。
要驗證其他用戶是否可以編輯您簽出的資產，請以其他用戶身份登錄。 表徵圖 ![簽出鎖定表徵圖](assets/do-not-localize/checkout_lock.png) 顯示在您簽出的資產的縮略圖上。

   ![卡視圖中的簽出表徵圖](assets/checkout-icon-card-view.png)

   選擇資產。 請注意，工具欄不顯示任何允許您編輯、注釋、發佈或刪除資產的選項。

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   要編輯鎖定資產的元資料，請按一下 **[!UICONTROL 查看屬性]**。

1. 按一下 **[!UICONTROL 編輯]** 以編輯模式開啟資源。

1. 編輯資產並保存更改。 例如，裁剪影像並保存。 您也可以選擇注釋或發佈資產。

1. 從 [!DNL Assets] ，然後按一下 **[!UICONTROL 簽入]** 的子菜單。 已修改的資產將簽入到 [!DNL Assets] 可供其他用戶編輯。

## 強制簽入 {#forced-check-in}

管理員可以簽入其他用戶簽出的資產。

1. 登錄到 [!DNL Assets] 作為管理員。
1. 從 [!DNL Assets] 用戶介面選擇一個或多個已由其他用戶簽出的資產。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具欄中，按一下 **[!UICONTROL 釋放鎖定]**。 資產將簽回並可供其他用戶編輯。

## 最佳做法和限制 {#tips-limitations}

* 可以刪除 *資料夾* 包含已簽出資產檔案。 在刪除資料夾之前，請確保用戶未簽出任何數字資產。

>[!MORELIKETHIS]
>
>* [了解籤入和簽出 [!DNL Experience Manager] 案頭應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [了解籤入和簽入的視頻教程 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

