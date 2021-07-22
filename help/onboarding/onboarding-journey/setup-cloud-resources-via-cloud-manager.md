---
title: 透過Cloud Manager設定雲端資源
description: 請依照本頁所述了解如何透過Cloud Manager設定雲端資源
hide: true
hidefromtoc: true
index: false
source-git-commit: 9caf3447fedf13fa81bb616cc54b7cb6a08ff159
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 0%

---

# 透過Cloud Manager設定雲端資源 {#setup-cloud-resources}

指派給&#x200B;*業務擁有者*&#x200B;角色的系統管理員應存取並登入Cloud Manager。 之後，指派給&#x200B;*業務擁有者*&#x200B;產品設定檔的團隊成員必須登入Cloud Manager並建立雲端程式和環境，才能開始使用您的專家團隊。

## 目標 {#objective}

本檔案可協助您了解雲端資源的建立方式，以及由誰執行。

閱讀本節後，您應了解：

* 指派給&#x200B;*業務擁有者*&#x200B;角色的系統管理員必須是第一個存取及登入Cloud Manager的管理員。
* 雲端程式和環境的建立方式。

## 簡介 {#introduction}

新增雲端資源是由指派給Cloud Manager業務擁有者產品設定檔的團隊成員透過Cloud Manager完成。 此人通常了解業務需求，並完成初始Cloud Manager設定。

請依照以下各節了解如何建立您的[雲端服務程式](#create-cloud-service-program)和[environments](#create-cloud-environments)。

### 先決條件 {#prerequisites}

* 指派給&#x200B;*業務擁有者*&#x200B;角色的系統管理員應存取並登入Cloud Manager。

* 了解如何[導覽並登入Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en)。

* 請熟悉[Cloud Manager產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)。

* 了解建立方案時的考量事項。 請觀看此影片以深入了解。

* 了解Cloud Manager [programs](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html?lang=en)和[environments](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en)的概念

## 導覽至Cloud Manager {#navigate-cloud-manager}

1. *業務擁有者*&#x200B;使用者會收到歡迎電子郵件，歡迎他們開始使用，或如果找不到，請直接前往[Adobe Experience Cloud](https://experience.adobe.com/#/@ccs/home)並使用您的Adobe ID登入。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources1.png)

1. 從Adobe Experience Cloud首頁，選擇&#x200B;**Experience Manager**。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources2.png)

1. 這會帶您前往AEM首頁。 從這裡啟動&#x200B;**Cloud Manager** 。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources3.png)

1. Cloud Manager登陸頁面隨即顯示，如下圖所示。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

1. 確認您已獲派「業務擁有者產品設定檔」。 若要這麼做，請從右上方選取您的設定檔，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources5.png)

1. 選擇&#x200B;**用戶角色**&#x200B;並確保您已分配給業務所有者。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources6.png)

1. 這可確認您的使用者角色為業務擁有者。

   ![](/help/onboarding/onboarding-journey/assets/setup-resources7.png)

   幹得好！ 您以業務擁有者身分成功登入Cloud Manager!

## 建立Cloud Service方案 {#create-cloud-service-program}

請依照下列步驟，從Cloud Manager建立您的雲端服務方案：

1. 導覽至Cloud Manager登陸頁面，如下所示。

   >[!NOTE]
   >您必須是指派給Cloud Manager業務擁有者產品設定檔的團隊成員，才能成功完成此步驟。

1. 從此處，選擇添加程式以啟動添加程式嚮導。 觀看影片，了解如何建立您的AEMaaCS計畫，以及在建立計畫前的重要考量。

1. 有關如何使用「添加程式」嚮導的逐步說明，請轉至此處。

   >[!CAUTION]
   >請記住，建立後無法更改程式名。 建議您確定要提供程式的名稱。

   如果您必須變更方案名稱，則需要開啟Adobe支援的案例，或聯絡您的Adobe代表。 他們將協助您有效刪除程式。 你必須重新開始，因為你的團隊可能會失去工作。

1. 成功建立雲端方案後，您可以導覽至方案，查看方案的概觀頁面，如下所示：

1. 如果您尚未這麼做，現在是將開發人員成員新增至Cloud Manager團隊的最佳時機，請前往「將使用者新增至開發人員產品設定檔」，並遵循概述的步驟。

1. 指派給開發人員產品設定檔的成員可登入Cloud Manager和Manage Cloud Manager Git。


   幹得好！ 現在程式已成功建立，您的Cloud Manager Git可供開發人員存取！


## 建立雲端環境 {#create-cloud-environments}

請依照下列步驟，從Cloud Manager建立您的雲端環境：

1. 成功建立雲端程式後，請導覽至Cloud Manager概觀頁面並從環境卡片中選取「新增」 ，以建立雲端環境。

   >[!IMPORTANT]
   >必須登入業務擁有者或部署管理員角色中的Cloud Manager使用者，才能成功完成此步驟。

   此外，請觀看快速影片教學課程，以了解Cloud Manager環境，以及如何將其新增至您的方案。

1. 這會啟動「新增環境」精靈，引導您新增環境。 先新增您的開發環境，以熟悉。

1. 如果您尚未這麼做，可以立即將開發人員成員新增至您的Cloud Manager團隊，前往「將使用者新增至開發人員產品設定檔」，並遵循概述的步驟。 如此一來，您的開發人員就能開始導覽至Cloud Manager及管理Cloud Manager Git。


   恭喜！ 現在，您的雲端程式環境已建立完畢，且您的開發人員已新增至團隊中！

## 下一步 {#whats-next}

您的團隊成員必須獲得執行個體的權限，因為管理Cloud Manager的權限不足。 現在，您的雲端資源已建立且可供您的團隊存取，系統管理員必須從Admin Console將您的團隊成員指派給AEM作為Cloud Service產品設定檔。

您應繼續進行入門歷程，接著檢閱將團隊成員指派給AEM as a Cloud Service產品設定檔的檔案。

>[!NOTE]
>若要以Cloud Service的身分授與AEM的存取權，使用者必須屬於「AEM使用者」或「AEM管理員」這兩個產品設定檔中的一個。 了解更多.

## 其他資源 {#additional-resources}

請依照其他資源了解：

* [程式類型和添加程式](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)
* [環境類型和新增環境](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en)
* [管理Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)
* [將AEM的存取權設為來自Admin Console的Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#adobe-ims-users)
