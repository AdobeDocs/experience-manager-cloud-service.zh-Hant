---
title: '將團隊成員指派給AEM作為Cloud Service產品設定檔 '
description: 請參照本頁面，了解如何將團隊成員指派給AEM as a Cloud Service產品設定檔
feature: Onboarding
role: Admin, User, Developer
source-git-commit: d8ff6f4386ab0e5df4f770cdb566facc1cc0cc98
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 2%

---


# 將團隊成員指派給AEM作為Cloud Service產品設定檔 {#assign-team-members-cloud-service}

## 目標 {#objective}

本檔案可協助您了解系統管理員必須執行哪些步驟，才能將您的團隊成員指派給AEM as a Cloud Service產品設定檔，以及為何讓AEM作者能夠透過AEM開始其歷程至關重要。

閱讀本節後，您應了解：

* 將您的團隊成員指派給AEM作為Cloud Service產品設定檔的原因及方式。
* 如何將團隊成員新增至AEM使用者產品設定檔。
* 如何將團隊成員新增至AEM管理員產品設定檔。


## 簡介 {#introduction}

若要以Cloud Service身分授與AEM的存取權，使用者必須屬於兩個產品設定檔之一： `AEM Users`或`AEM Administrators`。 您的團隊成員必須獲得AEM例項的權限，因為管理Cloud Manager的權限不足。

>[!NOTE]
>系統管理員指派給AEM User產品設定檔的每位使用者都擁有Cloud Manager的（唯讀）存取權。

## 先決條件 {#prerequisites}

開始閱讀本小節之前，您應先考慮下列先決條件：

* 了解[AEM as a Cloud Service產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)
* 熟悉[Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)
* Cloud Manager產品設定檔已視情況指派給您的團隊成員，且雲端資源已設定
* 有關您的團隊成員的詳細資訊：系統管理員必須擁有需要以Cloud Service方式存取AEM的團隊成員的姓名和電子郵件地址，以及角色和責任。

   >[!NOTE]
   >為了上線，建議您先新增將參與即時工作的使用者，例如管理員、開發人員和內容作者。 您可以繼續上線的其餘部分，而不需新增所有使用者。 上線完成後，您稍後可以擴充至更多使用者。


   >[!IMPORTANT]
   >開始檢閱將團隊成員指派給AEM as a Cloud Service產品設定檔的步驟之前，請務必遵循以下兩個步驟：
   >
   >1. 登入[Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)。 如需詳細資訊，請參閱登入Admin Console。
   >
   >1. 查看[AEM as a Cloud Service產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)。


請依照下列步驟，查看來自Adobe Admin Console的Cloud Manager設定檔清單：

1. 登入[Adobe Admin Console](https://adminconsole.adobe.com/)。 從&#x200B;**概述**&#x200B;頁面，從&#x200B;**產品和服務**&#x200B;卡中選擇&#x200B;**Adobe Experience Manager作為Cloud Service**。

   ![](/help/journey-onboarding/assets/assign-team1.png)

1. 導覽並選取例項（開發環境的製作例項），如下圖所示。

   ![](/help/journey-onboarding/assets/cloud-profiles-1.png)


1. 您會看到AEM清單，此為Cloud Service產品設定檔，需要根據使用者的角色指派給使用者。

   >[!NOTE]
   >若要深入了解這些設定，請參閱[AEM as a Cloud Service產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)。

   ![](/help/journey-onboarding/assets/cloud-profiles-2.png)


## 新增團隊成員至AEM使用者或AEM管理員產品設定檔 {#add-team-members}

若要以Cloud Service例項的形式授予AEM存取權，使用者必須屬於兩個產品設定檔`AEM Users`或`AEM Administrators`之一。

>[!NOTE]
>您必須獲得執行個體的權限，但管理Cloud Manager的權限不足。 了解更多.

下列步驟必須由同時處於業務所有者角色的系統管理員執行。

1. 從Cloud Manager導覽至您的程式，並從感興趣環境的內容中選取&#x200B;**管理存取**&#x200B;按鈕，如下所示。

   ![](/help/journey-onboarding/assets/add-team1.png)

1. 新索引標籤會從您存取環境的製作例項的位置，將您導覽至Adobe Admin Console。 根據此個人需要授予的權限，選取&#x200B;**AEM Administrators**&#x200B;或&#x200B;**AEM Users**。 進一步了解[AEM as aCloud Service產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#aem-product-profiles)。

   ![](/help/journey-onboarding/assets/add-team2.png)

1. 選擇`AEM Administrator`或`AEM User`，然後按一下&#x200B;**添加用戶**，如下所示，並提交必要的詳細資訊以完成添加團隊成員。

   ![](/help/journey-onboarding/assets/add-team3.png)

   您新增的使用者現在可以存取AEM作為Cloud Service作者服務！

   >[!NOTE]
   >如果您有需要存取權之團隊成員的資訊，您將想對所有環境（包括開發、預備和生產）重複執行這些步驟。


## 下一步 {#whats-next}

您指派給AEM as a Cloud Service產品設定檔的使用者現在已準備好了解如何存取「作者」，以及熟悉AEM as a Cloud Service中的編寫頁面。 您應該遵循此路徑，方法是接下來查看[AEM Users](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)或[Developers and Deployment Managers](/help/journey-onboarding/sysadmin/learning-path-developers-deploymentmanagers.md)的文檔學習路徑。

## 其他資源 {#additional-resources}

* [在 Admin Console 中管理產品和使用者存取權限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#managing-products-and-user-access-in-admin-console)
* [設定AEM存取權](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/walk-through.html?lang=en)
* [製作頁面的快速入門手冊](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/authoring/getting-started/quick-start.html?lang=en)