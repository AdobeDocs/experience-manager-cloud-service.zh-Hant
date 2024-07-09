---
title: 部署 [!DNL Content Hub]
description: 瞭解如何部署和啟用Content Hub，並為具有不同許可權型別的使用者(上傳資產、Adobe Express使用者)提供存取權，以及如何為使用者提供管理員許可權。
role: Admin
source-git-commit: 7224cca950e61bea298f246245bdb221fd8fa22e
workflow-type: tm+mt
source-wordcount: '1316'
ht-degree: 0%

---


# 部署 Content Hub {#deploy-content-hub}

![部署Content Hub](assets/deploy-content-hub.png)

Content Hub是Experience Manager Assets as a Cloud Service的一部分，可讓組織及其業務合作夥伴普及對品牌上內容的存取。

在Experience Manager Assetsas a Cloud Service上標示為已核准的資產可用於Content Hub上的資產發佈。

本文提供端對端工作流程，讓使用者可存取Content Hub，包括根據使用者的需求而變更的許可權。

Content Hub上的許可權變化包括：

* [Content Hub使用者](#onboard-content-hub-users)：在Content Hub入口網站上存取品牌核准的資產。

* [Content Hub管理員](#onboard-content-hub-administrator)：存取 [設定使用者介面](/help/assets/configure-content-hub-ui-options.md) 在Content Hub上，除了存取品牌核准資產、上傳資產至Content Hub、Adobe Express整合以編輯影像(如果您有Adobe Express許可權)。

* [有權新增資產的Content Hub使用者](#onboard-content-hub-users-add-assets)：功能 [將資產上傳至Content Hub](/help/assets/upload-brand-approved-assets.md) 除了存取Content Hub入口網站上的品牌核准資產之外。

* [有權將資產重新混合為新變數的Content Hub使用者](#onboard-content-hub-users-remix-assets)： [Adobe Express整合](/help/assets/edit-images-content-hub.md) (如果您有Adobe Express許可權)以及存取Content Hub入口網站上的品牌核准資產。

* [Experience Manager Assets使用者](#experience-manager-assets-users)：可在Experience Manager Assets上核准資產as a Cloud Service，以便這些資產可在Content Hub上使用。

## 步驟1：使用Cloud Manager啟用適用於Experience Manager Assets的Content Hub {#enable-content-hub}

若要存取Content Hub入口網站，管理員必須先使用Cloud Manager啟用適用於Experience Manager Assets的Content Hubas a Cloud Service。 執行以下步驟：

1. 登入Cloud Manager。 確保您在登入時選取正確的組織。 Cloud Manager會列出您的所有計畫。

1. 導覽至Experience Manager Assetsas a Cloud Service程式，按一下「更多選項」圖示(...)並選取 **[!UICONTROL 編輯計畫]**.

   ![在Cloud Manager中編輯程式](assets/edit-program-cloud-manager.png)

1. 在 [!UICONTROL 編輯計畫] 對話方塊中，選取 **[!UICONTROL 解決方案和附加元件]** 標籤。

1. 展開 **[!UICONTROL Assets]** 並選取 **[!UICONTROL Content Hub]**.
   ![在Cloud Manager中選取Content Hub](assets/edit-program-cloud-manager-content-hub.png)

   >[!NOTE]
   >
   >如果 **[!UICONTROL 更新]** 選擇Content Hub後沒有為您啟用，請確保您已指定該計畫的上線設定。

1. 按一下&#x200B;**[!UICONTROL 更新]**。

Content Hub現在已啟用Experience Manager Assetsas a Cloud Service。

>[!NOTE]
>
>您最多可以與250名Content Hub使用者存取和使用Content Hub。 如果您有其他問題，請聯絡您的Adobe代表。


如果您是Experience Manager Assets的新手，請按一下 **[!UICONTROL 新增計畫]** 然後提供計畫詳細資訊（計畫名稱、為生產設定）並按一下 **[!UICONTROL 繼續]**. 然後您可以選取 **[!UICONTROL Assets]** 和 **[!UICONTROL Content Hub]** 在 **[!UICONTROL 解決方案和附加元件]** 標籤。

### Admin Console上的Content Hub執行個體和產品設定檔{#content-hub-instance-product-profile}

晚於 [使用Cloud Manager為Assetsas a Cloud Service啟用Content Hub](#enable-content-hub)，即會在AEM Assets中建立新的執行個體(as a Cloud Service於的Admin Console) `contenthub` 做為尾碼：

![Content Hub的新執行個體](assets/new-instance-content-hub.png)

請注意，沒有 `author` 或 `publish` 在Content Hub的執行個體名稱中。

按一下執行個體名稱以檢視Content Hub產品設定檔。

![Content Hub產品設定檔](assets/content-hub-product-profile.png)

## 步驟2：加入Content Hub管理員 {#onboard-content-hub-administrator}

Content Hub管理員可以存取 [設定使用者介面](/help/assets/configure-content-hub-ui-options.md) 在Content Hub上，除了存取品牌核准資產、上傳資產至Content Hub、Adobe Express整合以編輯影像(如果您有Adobe Express許可權)。

若要加入Content Hub管理員：

1. [存取並按一下Content Hub使用者產品設定檔](#content-hub-instance-product-profile).

1. 按一下 **[!UICONTROL 新增使用者]** 將使用者或使用者群組新增至產品設定檔。

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。

1. 將使用者新增到Content Hub產品設定檔後，請按一下Admin Console上產品清單中的AEM as a Cloud Service產品名稱來存取Experience Manager Assets產品設定檔。

1. 按一下AEM as a Cloud Service的生產製作例項：
   ![AEM as a Cloud Service的產品設定檔](assets/aem-cloud-service-instances.png)

   Admin Console會顯示AEM as a Cloud Service的兩個產品設定檔：管理員和使用者。
1. 按一下管理員產品設定檔，然後按一下 **[!UICONTROL 新增使用者]** 將使用者新增至產品設定檔。
   ![管理員產品設定檔](assets/aem-cs-admin-product-profile.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。

## 步驟3：入門Content Hub使用者 {#onboard-content-hub-users}

Content Hub使用者可以存取入口網站上的可用資產，但無法新增任何資產或修改現有資產。

若要加入Content Hub使用者：

1. [存取並按一下Content Hub使用者產品設定檔](#content-hub-instance-product-profile).

1. 按一下 **[!UICONTROL 新增使用者]** 將使用者或使用者群組新增至產品設定檔。

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。

這些使用者現在可以存取Content Hub入口網站上的可用資產。

>[!NOTE]
>
>您可以使用所有進階企業功能，例如與外部識別提供者同步化。

### 如何存取Content Hub？ {#access-content-hub}

Content Hub的存取方式如下：

* 使用下列連結存取Content Hub：

  `https://experience.adobe.com/#/assets/contenthub`

* 登入 `experience.adobe com` 並按一下 **[!UICONTROL Experience Manager Assets Content Hub]** 可在 **[!UICONTROL 快速存取]** 區段：
  ![Content Hub存取](assets/access-content-hub.png)

* 登入 `experience.adobe com` 並按一下 **[!UICONTROL Experience Manager Assets Content Hub]** 可在產品切換器中取得：
  ![Content Hub存取方法3](assets/access-content-hub-alternate.png)

### 停用使用者的電子郵件通知 {#disable-email-notifications}

如果管理員需要在將使用者新增至Content Hub產品設定檔時停用傳送給使用者的電子郵件通知：

按一下產品設定檔名稱旁的搜尋圖示，並停用 **[!UICONTROL 透過電子郵件通知使用者]** 切換。

![停用電子郵件通知](assets/disable-email-notifications.png)


## 步驟4：新增Content Hub使用者並取得資產許可權（選用） {#onboard-content-hub-users-add-assets}

有權新增資產的Content Hub使用者可以 [將品牌核准的新資產上傳到Content Hub](/help/assets/upload-brand-approved-assets.md).

若要讓具有新增使用者許可權的Content Hub使用者上線：

1. [將使用者新增到Content Hub產品設定檔後](#onboard-content-hub-users)，請按一下Admin Console上產品清單中的Experience Manager Assets產品名稱來存取AEM as a Cloud Service產品設定檔。

1. 按一下AEM as a Cloud Service的生產製作例項：
   ![AEM as a Cloud Service的產品設定檔](assets/aem-cloud-service-instances.png)

   Admin Console會顯示AEM as a Cloud Service的兩個產品設定檔：管理員和使用者。
1. 按一下「使用者」產品設定檔，然後按一下 **[!UICONTROL 新增使用者]** 將使用者新增至產品設定檔。
   ![使用者產品設定檔](assets/aem-cs-user-product-profile.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。

## 步驟4：加入Content Hub使用者，並有權將資產重新混合成新的變數（選用） {#onboard-content-hub-users-remix-assets}

有權將資產重新混合到新變數的Content Hub使用者可以 [使用Adobe Express修改現有資產並將資產儲存至存放庫](/help/assets/edit-images-content-hub.md). 只有使用者擁有Adobe Express權益，才能使用Adobe Express編輯資產。

若要讓有權將資產重新混合為新變數的Content Hub使用者上線：

1. [將使用者新增到Content Hub產品設定檔後](#onboard-content-hub-users)，請按一下Admin Console上產品清單中的Experience Manager Assets產品名稱來存取AEM as a Cloud Service產品設定檔。

1. 按一下AEM as a Cloud Service的生產製作例項：
   ![AEM as a Cloud Service的產品設定檔](assets/aem-cloud-service-instances.png)

   Admin Console會顯示AEM as a Cloud Service的兩個產品設定檔：管理員和使用者。
1. 按一下「使用者」產品設定檔，然後按一下 **[!UICONTROL 新增使用者]** 將使用者新增至產品設定檔。
   ![使用者產品設定檔](assets/aem-cs-user-product-profile.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。

## Experience Manager Assets使用者 {#experience-manager-assets-users}

Experience Manager Assets使用者可以在AEM as a Cloud Service上核准資產，以便在Content Hub上使用。

若要設定Experience Manager Assets使用者：

1. 按一下Admin Console上產品清單中的Experience Manager Assets產品名稱，存取AEM as a Cloud Service產品設定檔。

1. 按一下AEM as a Cloud Service的生產製作例項：
   ![AEM as a Cloud Service的產品設定檔](assets/aem-cloud-service-instances.png)

   Admin Console會顯示AEM as a Cloud Service的兩個產品設定檔：管理員和使用者。
1. 按一下「使用者」產品設定檔，然後按一下 **[!UICONTROL 新增使用者]** 將使用者新增至產品設定檔。
   ![使用者產品設定檔](assets/aem-cs-user-product-profile.png)

1. 按一下 **[!UICONTROL 儲存]** 以儲存變更。

   >[!NOTE]
   >
   > 您不需要新增至 [Content Hub產品設定檔](#onboard-content-hub-users) 適用於Experience Manager Assets使用者。



