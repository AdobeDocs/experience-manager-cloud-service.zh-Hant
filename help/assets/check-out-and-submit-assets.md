---
title: 簽入和簽出 [!DNL Assets]中的檔案
description: 了解如何簽出要編輯的資產，並在變更完成後重新簽入。
contentOwner: AG
feature: 資產管理
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: a2c2a1f4ef4a8f0cf1afbba001d24782a6a2a24e
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# [!DNL Experience Manager] DAM中的簽入和簽出檔案 {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] 可讓您簽出要編輯的資產，並在完成變更後重新簽入。結帳資產後，只有您可以編輯、注釋、發佈、移動或刪除資產。 簽出資產會鎖定資產。 在您將資產簽回[!DNL Assets]之前，其他使用者無法對資產執行任何這些操作。 不過，他們仍可以變更鎖定資產的中繼資料。

若要簽出/登入資產，您需要這些資產的寫入存取權。

此功能可協助防止其他使用者覆寫作者所做的變更，讓多位使用者共同合作編輯團隊間的工作流程。

## 結帳資產 {#checking-out-assets}

1. 從[!DNL Assets]使用者介面中，選取您要結帳的資產。 您也可以選取多個要結帳的資產。

1. 在工具列中，按一下&#x200B;**[!UICONTROL Checkout]**。 **[!UICONTROL Checkout]**&#x200B;選項切換為&#x200B;**[!UICONTROL Checkin]**。
若要確認其他使用者是否可以編輯您簽出的資產，請以其他使用者身分登入。 圖示![結帳鎖定圖示](assets/do-not-localize/checkout_lock.png)會顯示在您結帳的資產縮圖上。

   ![卡片檢視中的結帳圖示](assets/checkout-icon-card-view.png)

   選取資產。 請注意，工具列不會顯示任何選項，讓您編輯、注釋、發佈或刪除資產。

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   若要編輯鎖定資產的中繼資料，請按一下「檢視屬性&#x200B;****」。

1. 按一下「**[!UICONTROL 編輯]**」以在編輯模式中開啟資產。

1. 編輯資產並儲存變更。 例如，裁切影像並儲存。 您也可以選擇為資產加上注釋或發佈。

1. 從[!DNL Assets]介面中選擇已編輯的資產，然後從工具欄按一下&#x200B;**[!UICONTROL 簽入]**。 已修改的資產已簽入[!DNL Assets]，可供其他使用者編輯。

## 強制簽入 {#forced-check-in}

管理員可以簽入其他用戶簽出的資產。

1. 以管理員身分登入[!DNL Assets]。
1. 從[!DNL Assets]使用者介面中，選取一或多個已由其他使用者簽出的資產。

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. 在工具欄中，按一下&#x200B;**[!UICONTROL 釋放鎖定]**。 資產會重新簽入，供其他使用者編輯。

## 最佳實務和限制 {#tips-limitations}

* 可以刪除包含已簽出資產檔案的&#x200B;*資料夾*。 刪除資料夾前，請確定使用者未簽出任何數位資產。

>[!MORELIKETHIS]
>
>* [了解籤入和簽出獨立頂 [!DNL Experience Manager] 層應用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#how-app-works2)
>* [了解籤入和簽出的視頻教程 [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

