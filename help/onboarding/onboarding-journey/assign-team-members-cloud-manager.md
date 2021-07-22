---
title: '將團隊成員指派給Cloud Manager產品設定檔 '
description: 請詳閱本頁，了解如何將團隊成員指派給Cloud Manager產品設定檔
hide: true
hidefromtoc: true
index: false
source-git-commit: 3dbcc5dd09479a84ed13aad0ee3d8c229520e10f
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 0%

---


# 將團隊成員指派給Cloud Manager產品設定檔 {#assign-team-members}

學習如何登入[Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)並以[系統管理員](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/system-administrator.html?lang=en)身分檢視您的權限後，您現在可以將團隊成員指派給Cloud Manager產品設定檔。

## 目標 {#objective}

本檔案概述如何從Admin Console將團隊成員指派給Cloud Manager產品設定檔。

閱讀本小節後，您應能：

* 了解您必須新增團隊成員的原因及方式。
* 了解3種不同的Cloud Manager產品設定檔，例如業務擁有者、部署管理員和開發人員。
* 將團隊成員指派給Cloud Manager產品設定檔，例如業務擁有者、部署管理員和開發人員。

## 必備條件 {#prerequisites}

開始本節之前，應考慮下列必要條件。 您必須是：

* 系統管理員並了解[Cloud Manager產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)。
* 了解[Adobe Admin Console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/admin-console.html?lang=en)基本知識。
* 必須有關於團隊成員的詳細資訊。 系統管理員必須擁有需要以Cloud Service方式存取AEM的團隊成員的姓名和電子郵件地址，以及角色和責任。

   >[!NOTE]
   >為了上線，建議您先新增將參與即時工作的使用者，例如管理員、開發人員和內容作者。 您可以繼續上線的其餘部分，而不需新增所有使用者。 上線完成後，您稍後可以擴充至更多使用者。

## 檢閱Cloud Manager產品設定檔 {#review-product-profiles}

從Admin Console中，您可以看到Cloud Manager設定檔清單。

>[!NOTE]
>在您從Admin Console查看Cloud Manager產品設定檔之前，建議您先檢閱可用的[Cloud Manager產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)。

請依照下列步驟檢視Cloud Manager設定檔清單：

1. 登入[Adobe Admin Console](https://adminconsole.adobe.com/)。 從&#x200B;**概述**&#x200B;頁面，從&#x200B;**產品和服務**&#x200B;卡中選擇&#x200B;**Adobe Experience Manager作為Cloud Service**。

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

   >[!NOTE]
   >請參閱登入Admin Console，了解如何使用Admin Console。


1. 從表格導覽至&#x200B;**Cloud Manager**&#x200B;例項，並列出所有例項。

   ![](/help/onboarding/onboarding-journey/assets/assign-team2.png)

1. 您會看到預先設定的[Cloud Manager產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)清單。

   ![](/help/onboarding/onboarding-journey/assets/assign-team3.png)


## 將用戶分配給業務所有者產品配置檔案 {#assign-users-business-owner}

您現在可以新增使用者，並將其指派給Cloud Manager Business Owner產品設定檔。

>[!NOTE]
>為了成功執行此作業，您必須從Admin Console將使用者新增至產品(在此為Cloud Service的AEM)和[Cloud Manager業務擁有者產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)。

下列步驟將引導您完成此操作：

1. 識別將管理Cloud Manager程式的使用者，並將他們新增至業務擁有者產品設定檔。 系統管理員必須是第一個存取及登入Cloud Manager的人員。 您必須先將自己（系統管理員）添加到業務所有者產品配置檔案中。

1. 在[Admin Console](https://adminconsole.adobe.com/enterprise/overview) **概述**&#x200B;頁面中，從&#x200B;**產品與服務**&#x200B;卡中選擇&#x200B;**Adobe Experience Manager作為Cloud Service**&#x200B;產品，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. 從頂部導航中選擇&#x200B;**用戶**&#x200B;頁簽，然後選擇&#x200B;**添加用戶**。

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. 在&#x200B;**將使用者新增至您的團隊**&#x200B;對話方塊中，輸入您要新增之使用者的電子郵件ID。 如果尚未設定團隊成員的Federated ID，請為「ID類型」選取「Adobe ID」。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. 在「產品」選項中，選擇&#x200B;**Adobe Experience Manager作為Cloud Service**，並將&#x200B;**業務所有者**&#x200B;產品配置檔案分配給用戶，如下所示。

   >[!NOTE]
   >請參閱[Cloud Manager產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)，確保在Admin Console中為正確的使用者指派正確的角色，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

   >[!NOTE]
   >將使用者指派至少一個產品設定檔，讓使用者可以存取Cloud Manager。 請記得將您自己（系統管理員）指派給業務擁有者。

1. 按一下「**儲存**」。歡迎電子郵件會傳送給您新增的使用者。 受邀的使用者可按一下歡迎電子郵件中的連結，並使用其Adobe ID登入，以存取Cloud Manager。

恭喜！ 現在，您新組建的Cloud Manager團隊（包括您自己指派給「業務擁有者」角色的團隊）已完成設定。 會員會收到歡迎電子郵件，邀請他們登入並存取Cloud Manager。 在業務擁有者角色中，您現在只需一步即可登入Cloud Manager並啟用雲端資源的建立。

## 將用戶分配到Deployment Manager產品配置檔案 {#assign-users-deployment-manager}

1. 識別將管理Cloud Manager程式的使用者，並將他們新增至Deployment Manager產品設定檔。 系統管理員必須是第一個存取及登入Cloud Manager的人員。 您必須先將自己（系統管理員）添加到業務所有者產品配置檔案中。

1. 在[Admin Console](https://adminconsole.adobe.com/enterprise/overview) **概述**&#x200B;頁面中，從&#x200B;**產品與服務**&#x200B;卡中選擇&#x200B;**Adobe Experience Manager作為Cloud Service**&#x200B;產品，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. 從頂部導航中選擇&#x200B;**用戶**&#x200B;頁簽，然後選擇&#x200B;**添加用戶**。

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. 在&#x200B;**將使用者新增至您的團隊**&#x200B;對話方塊中，輸入您要新增之使用者的電子郵件ID。 如果尚未設定團隊成員的Federated ID，請為「ID類型」選取「Adobe ID」。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. 在「產品」選項中，選擇&#x200B;**Adobe Experience Manager作為Cloud Service**，並將&#x200B;**Deployment Manager**&#x200B;產品配置檔案分配給用戶，如下所示。

   >[!NOTE]
   >請參閱[Cloud Manager產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)，確保在Admin Console中為正確的使用者指派正確的角色，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)。

   >[!IMPORTANT]
   >建立Cloud Manager資源後，可將使用者新增至Deployment Manager產品設定檔。

## 將使用者指派給開發人員產品設定檔 {#assign-users-developer}

1. 識別將管理Cloud Manager程式的使用者，並將他們新增至開發人員產品設定檔。 系統管理員必須是第一個存取及登入Cloud Manager的人員。 您必須先將自己（系統管理員）添加到業務所有者產品配置檔案中。

1. 在[Admin Console](https://adminconsole.adobe.com/enterprise/overview) **概述**&#x200B;頁面中，從&#x200B;**產品與服務**&#x200B;卡中選擇&#x200B;**Adobe Experience Manager作為Cloud Service**&#x200B;產品，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team1.png)

1. 從頂部導航中選擇&#x200B;**用戶**&#x200B;頁簽，然後選擇&#x200B;**添加用戶**。

   ![](/help/onboarding/onboarding-journey/assets/assign-team4.png)

1. 在&#x200B;**將使用者新增至您的團隊**&#x200B;對話方塊中，輸入您要新增之使用者的電子郵件ID。 如果尚未設定團隊成員的Federated ID，請為「ID類型」選取「Adobe ID」。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)

1. 在「產品」選項中，選擇&#x200B;**Adobe Experience Manager作為Cloud Service**，並將&#x200B;**Developer**&#x200B;產品配置檔案分配給用戶，如下所示。

   >[!NOTE]
   >請參閱[Cloud Manager產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)，確保在Admin Console中為正確的使用者指派正確的角色，如下所示。

   ![](/help/onboarding/onboarding-journey/assets/assign-team5.png)。


   >[!IMPORTANT]
   >建立Cloud Manager資源後，可將使用者新增至開發人員產品設定檔。

## 下一步 {#whats-next}

作為分配給&#x200B;*業務所有者*&#x200B;角色的系統管理員，您必須訪問並登錄Cloud Manager。
>[!NOTE]
>請參閱[導覽至Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en) ，了解如何登入及存取Cloud Manager。

業務擁有者角色中的Cloud Manager使用者可登入並設定您的雲端資源，包括您的方案和環境。 這可確保您的專家團隊能盡快開始以Cloud Service存取AEM。
業務擁有者設定雲端資源後，已成功新增至Cloud Manager產品設定檔的開發人員和部署經理可以存取Cloud Manager，並熟悉如何繼續學習。

## 其他資源 {#additional-resources}

請依照其他資源了解：

* [Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html?lang=en)
* [Cloud Manager產品設定檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles)
* [Admin Console身分概述](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/identity.ug.html)
