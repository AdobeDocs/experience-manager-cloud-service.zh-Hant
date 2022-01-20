---
title: 通過雲管理器設定雲資源
description: 按照本頁瞭解如何通過雲管理器設定雲資源
role: Admin, User, Developer
exl-id: de3a33b7-b459-4e47-b232-a0f88e2ce22e
source-git-commit: 7fe39bbc8d5e965af7f339b2a524420c76360552
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# 通過雲管理器設定雲資源 {#setup-cloud-resources}

分配給業務所有者角色的系統管理員應訪問並登錄雲管理器。 此後，分配給業務所有者產品配置檔案的團隊成員必須登錄到雲管理器並建立您的雲程式和環境，以便您的專家團隊能夠開始。

## 目標 {#objective}

此文檔可幫助您瞭解雲資源是如何建立的以及誰可以建立雲資源。

讀完本節後，您應瞭解：

* 分配給「業務所有者」角色的系統管理員必須是第一個訪問和登錄雲管理器的管理員。
* 如何建立雲程式和環境。

## 簡介 {#introduction}

添加雲資源是通過Cloud Manager完成的，您的團隊成員已分配給Cloud Manager Business Owner產品配置檔案。 此人通常是瞭解業務需求並完成初始雲管理器安裝的人員。

請按照以下部分瞭解如何建立 [雲服務程式](#create-cloud-service-program) 和 [環境。](#create-cloud-environments)

### 先決條件 {#prerequisites}

* 分配給業務所有者角色的系統管理員應訪問並登錄雲管理器。

* 瞭解如何 [導航並登錄到Cloud Manager。](/help/onboarding/learn-concepts/cloud-manager-introduction.md)

* 熟悉 [Cloud Manager產品配置檔案。](/help/onboarding/learn-concepts/aem-cs-team-product-profiles.md#cloud-manager-product-profiles)

* 瞭解雲管理器的概念 [方案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/understand-program-types.md) 和 [環境。](/help/implementing/cloud-manager/manage-environments.md)

## 導航到雲管理器 {#navigate-cloud-manager}

業務所有者用戶將收到一封歡迎電子郵件，其中包含要開始使用的連結，或者如果他們找不到，則訪問 [雲管理器](https://my.cloudmanager.adobe.com/) 直接用你的Adobe ID登錄。

按照以下步驟導航至Cloud Manager:

1. 從歡迎電子郵件中按一下 **開始**，如下圖所示。
   ![](/help/journey-onboarding/assets/get-started-email.png)

1. 您將導航至Cloud Manager **計畫和產品** 的子菜單。

   >[!IMPORTANT]
   >
   >或者，您也可以直接從Cloud Manager的登錄頁導航 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)。 請將此頁面加入書籤以供將來參考，並幫助您直接導航至Cloud Manager的登錄頁。

1. 您將被定向到Cloud Manager的登錄頁。 請參閱 [查看雲管理器的程式](#viewing-programs) 的子菜單。

此外，您還可以導航至Cloud Manager的 **計畫和產品** Adobe Experience Cloud首頁。 請遵循下列步驟：

1. 直接導航到 [Adobe Experience Cloud](https://experience.adobe.com) 用你的Adobe ID登錄。

1. 從Adobe Experience Cloud首頁，選擇 **Experience Manager**。

   ![](/help/journey-onboarding/assets/setup-resources2.png)

1. 這會帶你到主AEM頁。 從這裡，發射 **雲管理器** 。

   ![](/help/journey-onboarding/assets/setup-resources3.png)

1. 成功登錄後，您將被定向到Cloud Manager的登錄頁。 請參閱 [查看雲管理器的程式](#viewing-programs) 的子菜單。

   >[!NOTE]
   >
   >根據在中分配的角色 [!UICONTROL 雲管理器] 以及應用程式的狀態，在使用 [!UICONTROL 雲管理器] UI。

### 在雲管理器登錄頁中查看程式 {#viewing-programs}

成功登錄後，您將被定向到Cloud Manager的登錄頁。 您將看到以下三個選項之一：

#### 當雲管理器中不存在程式時 {#no-programs}

如果組織中不存在程式，則登錄頁會指示您建立第一個程式，如下圖所示。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

#### 當雲管理器中已存在程式時 {#programs-exist}

如果您的組織中已存在程式，則登錄頁會指示您添加另一個程式並顯示所有現有程式，如下圖所示。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

#### 當程式存在且用戶是系統管理員時 {#programs-exist-sysadmin}

如果您的組織中已存在程式，並且您是系統管理員，則將顯示登錄頁 **管理訪問** 按鈕 **添加程式** 的下界。

![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)


## 驗證用戶角色 {#verify-user-roles}

成功登錄雲管理器後，請按照以下步驟驗證是否已為您分配了業務所有者產品配置檔案：

1. 從右上角選擇您的配置檔案，如下所示。

   ![](/help/journey-onboarding/assets/setup-resources5.png)

1. 選擇 **用戶角色** 並確保您已分配給業務所有者。

   ![](/help/journey-onboarding/assets/setup-resources6.png)

1. 這將確認您作為業務所有者的用戶角色。

   ![](/help/journey-onboarding/assets/setup-resources7.png)

   幹得好！ 您已以業務所有者身份成功登錄到雲管理器！

## 建立Cloud Service程式 {#create-cloud-service-program}

按照以下步驟從Cloud Manager建立雲服務程式：

1. 導航至Cloud Manager登錄頁，如下所示。

   >[!NOTE]
   >
   >您必須是分配給Cloud Manager業務所有者產品配置檔案的團隊成員才能成功完成此步驟。

   在此處，按一下 **添加程式** 啟動「添加程式」嚮導。

   ![](/help/journey-onboarding/assets/setup-resources4.png)

   >[!TIP]
   >
   >觀看 [視頻](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) 瞭解如何將您建立AEM為雲程式，並在建立程式之前瞭解重要注意事項。

   >[!TIP]
   >
   >有關如何使用「添加程式」嚮導的逐步說明，請轉至 [這裡](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-program.md)。

1. 成功建立雲程式後，您可以導航到程式以查看 **概述** 頁面，如下所示。

   ![](/help/journey-onboarding/assets/setup-resources8.png)

   >[!NOTE]
   >
   >如果您尚未這樣做，現在是將開發人員成員添加到雲管理器團隊的好時機。 請參閱將用戶添加到開發人員產品配置檔案，並按照概述的步驟操作。

1. 分配給開發人員產品配置檔案的成員可以登錄到Cloud Manager, [管理雲管理器Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)。

   幹得好！ 現在，您的程式已成功建立，您的雲管理器Git可供開發人員訪問！


## 建立雲環境 {#create-cloud-environments}

成功建立雲程式後，請建立雲環境。

按照以下步驟從Cloud Manager建立雲環境：

1. 導航至雲管理器 **概述** 選擇 **添加** 從環境卡上。

   ![](/help/journey-onboarding/assets/setup-resources9.png)

   >[!IMPORTANT]
   >
   >必須登錄業務所有者或部署管理器角色中的雲管理器用戶才能成功完成此步驟。

   另外，請觀察 [視頻](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html) 教程，瞭解有關Cloud Manager環境以及如何將它們添加到程式中。

1. 這將啟動添加環境嚮導，該嚮導將指導您完成添加環境的過程。 首先添加開發環境以熟悉嚮導。 請參閱 [添加環境](/help/implementing/cloud-manager/manage-environments.md#adding-environments) 來瞭解更多資訊。

   >[!NOTE]
   >
   >如果您尚未這樣做，現在是將開發人員成員添加到雲管理器團隊的好時機。 請參閱將用戶添加到開發人員產品配置檔案，並按照概述的步驟操作。

1. 分配給開發人員產品配置檔案的成員可以登錄到Cloud Manager, [管理Cloud Manager Git。](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

   幹得好！ 現在，您的程式已成功建立，並且您的Cloud Manager Git可供開發人員訪問！

   恭喜！ 現在，您的雲程式環境已建立並且開發人員已添加到團隊中！

## 下一步是什麼 {#whats-next}

您的團隊成員必須被授予該實例的權限，因為管理雲管理器的權限是不夠的。 既然雲資源已建立並準備好由您的團隊訪問，系統管理員必須將您的團隊成員分配給Adobe Admin Console的AEMas a Cloud Service產品配置檔案。

>[!NOTE]
>
>要授予對as a Cloud Service用AEM戶的訪問權限，必須屬於兩個產品配置檔案之一 `AEM Users` 或 `AEM Administrators`。 請參閱 [在Admin Console中管理產品和用戶訪問](/help/security/ims-support.md#managing-products-and-user-access-in-admin-console) 來瞭解更多資訊。

您應通過下次查看文檔來繼續登機旅程 [為as a Cloud Service產品配置AEM檔案分配團隊成員。](/help/journey-onboarding/sysadmin/assign-team-members-aem-cloud-service.md)


## 其他資源 {#additional-resources}

按照其他資源瞭解：

* [程式類型和添加程式](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html)
* [環境類型和添加環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html)
* [管理雲管理器Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)
* [配置對AEMas a Cloud Service的訪問](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html#adobe-ims-users)
