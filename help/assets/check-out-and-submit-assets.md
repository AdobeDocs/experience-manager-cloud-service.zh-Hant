---
title: 資產中的登入和登出檔案
description: 瞭解如何取出要編輯的資產，並在變更完成後將其存回。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 4%

---


# 資產中的登入和登出檔案 {#check-in-and-check-out-files-in-assets}

Adobe Experience Manager(AEM)Assets可讓您取出要編輯的資產，並在完成變更後將其存回。 結帳資產後，只有您可以編輯、註解、發佈、移動或刪除資產。 簽出資產會鎖定資產。 其他使用者無法對資產執行任何這些作業，直到您將資產存回AEM Assets。 不過，他們仍可變更鎖定資產的中繼資料。

若要能夠登出／登入資產，您需要有其「寫入」存取權。

此功能可協助防止其他使用者覆寫作者所做的變更，讓多位使用者在跨團隊編輯工作流程時共同作業。

## 結帳資產 {#checking-out-assets}

1. 從「資產」使用者介面中，選取您要結帳的資產。 您也可以選取多個資產以結帳。

   ![chlimage_1-468](assets/chlimage_1-468.png)

1. 在工具列中，按一下／點選「結 **[!UICONTROL 帳]** 」圖示。

   ![chlimage_1-469](assets/chlimage_1-469.png)

   請注意，「 **[!UICONTROL Checkout]** （檢出）」表徵圖在開啟鎖的情況下切換到「 **[!UICONTROL Checkin]** （檢入）」表徵圖。

   ![chlimage_1-470](assets/chlimage_1-470.png)

   若要確認其他使用者是否可以編輯您簽出的資產，請以其他使用者的身分登入。 鎖定圖示會出現在您已簽出的資產的縮圖上。

   ![chlimage_1-471](assets/chlimage_1-471.png)

   選取資產。 請注意，工具列不會顯示任何選項，讓您編輯、註解、發佈或刪除資產。

   ![chlimage_1-472](assets/chlimage_1-472.png)

   不過，您可以按一下／點選「檢 **[!UICONTROL 視屬性」圖示]** ，編輯已鎖定資產的中繼資料。

1. 按一下／點選「編輯」圖示，以在編輯模式中開啟資產。

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. 編輯資產並儲存變更。 例如，裁切影像並儲存。

   ![chlimage_1-474](assets/chlimage_1-474.png)

   您也可以選擇註解或發佈資產。

1. 從「資產」UI中選取已編輯的資產，然後按一下/點選工具列中的「 **[!UICONTROL 登入]** 」圖示。

   ![chlimage_1-475](assets/chlimage_1-475.png)

   已修改的資產會登入AEM Assets，可供其他使用者編輯。

## 強制登入 {#forced-check-in}

管理員可以簽入由其他用戶簽出的資產。

1. 以管理員身分登入AEM Assets。
1. 從「資產」使用者介面中，選取一或多個已由其他使用者簽出的資產。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具列中，按一下／點選「 **[!UICONTROL 釋放鎖定]** 」圖示。 資產已登入，可供其他使用者編輯。

   ![chlimage_1-477](assets/chlimage_1-477.png)