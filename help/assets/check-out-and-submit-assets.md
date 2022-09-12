---
title: 簽入和簽出檔案 [!DNL Assets]
description: 了解如何簽出要編輯的資產，並在變更完成後重新簽入。
contentOwner: AG
feature: Asset Management
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: 034899c2a717fafdc50cc269d6db3feb77d907c5
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# 簽入和簽出檔案 [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] 可讓您簽出要編輯的資產，並在完成變更後重新簽入。 結帳資產後，只有您可以編輯、注釋、發佈、移動或刪除資產。 簽出資產會鎖定資產。 在您將資產簽回 [!DNL Assets]. 不過，他們仍可以變更鎖定資產的中繼資料。

若要簽出/登入資產，您需要這些資產的寫入存取權。

此功能可協助防止其他使用者覆寫作者所做的變更，讓多位使用者共同合作編輯團隊間的工作流程。

## 結帳資產 {#checking-out-assets}

1. 從 [!DNL Assets] 使用者介面，選取您要結帳的資產。 您也可以選取多個要結帳的資產。

1. 在工具列中，按一下 **[!UICONTROL 結帳]**. 此 **[!UICONTROL 結帳]** 選項切換為 **[!UICONTROL 簽入]**.
若要確認其他使用者是否可以編輯您簽出的資產，請以其他使用者身分登入。 圖示 ![簽出鎖定表徵圖](assets/do-not-localize/checkout_lock.png) 會顯示在您簽出的資產縮圖上。

   ![卡片檢視中的結帳圖示](assets/checkout-icon-card-view.png)

   選取資產。 請注意，工具列不會顯示任何選項，讓您編輯、注釋、發佈或刪除資產。

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   若要編輯鎖定資產的中繼資料，請按一下 **[!UICONTROL 檢視屬性]**.

1. 按一下 **[!UICONTROL 編輯]** 以在編輯模式中開啟資產。

1. 編輯資產並儲存變更。 例如，裁切影像並儲存。 您也可以選擇為資產加上注釋或發佈。

1. 從 [!DNL Assets] 介面，然後按一下 **[!UICONTROL 簽入]** 的上界。 已修改的資產會簽入至 [!DNL Assets] 和可供其他使用者編輯。

## 強制簽入 {#forced-check-in}

管理員可以簽入其他用戶簽出的資產。

1. 登入 [!DNL Assets] 管理員。
1. 從 [!DNL Assets] 使用者介面會選取一或多個已由其他使用者簽出的資產。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具列中，按一下 **[!UICONTROL 釋放鎖]**. 資產會重新簽入，供其他使用者編輯。

## 最佳實務和限制 {#tips-limitations}

* 可以刪除 *資料夾* 包含已簽出的資產檔案。 刪除資料夾前，請確定使用者未簽出任何數位資產。

>[!MORELIKETHIS]
>
>* [了解籤入和簽入 [!DNL Experience Manager] 案頭應用程式](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [了解籤入和簽出的視頻教程 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

