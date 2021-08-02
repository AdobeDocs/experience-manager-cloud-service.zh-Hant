---
title: 導覽至Cloud Manager
description: 請依照本頁面所述，了解如何導覽至Cloud Manager登陸頁面
exl-id: 9cf25d1d-a351-4ea0-b2e9-1df6ca4915b7
source-git-commit: e7f8e7daa88c5bf8bb13c2a635fb84724f8bd7bb
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 6%

---

# 導覽至Cloud Manager {#cloud-manager}

Cloud Manager是AEM as a Cloud Service的重要一環。 它可讓組織在雲端中自行管理Experience Manager。 其內容包含持續整合與持續傳送 (CI/CD) 架構，可讓 IT 團隊與實作合作夥伴加快提供自訂或更新的傳送速度，而不會影響效能或安全性。使用者介面，您可以設定並啟動CI/CD管道。

一旦系統管理員授予您Cloud Manager的存取權，您會收到電子郵件，將帶您前往[Adobe Experience Cloud](https://experience.adobe.com)首頁。

>[!NOTE]
>您必須新增為使用者，且系統管理員必須至少將您指派給一個Cloud Manager角色(Admin Console中的產品設定檔)。

1. 在歡迎電子郵件中，按一下&#x200B;**Get started**，如下圖所示。
   ![](/help/onboarding/what-is-required/assets/get-started-email.png)

   >[!NOTE]
   >或者，您也可以從[my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)直接導覽至Cloud Manager登入頁面。 根據在[!UICONTROL Cloud Manager]中指派的角色和應用程式的狀態，使用[!UICONTROL Cloud Manager] UI時會看到不同的畫面。 如需詳細資訊，請參閱以下的[Cloud Manager登陸頁面](#cloud-manager-landing)一節。

1. 選擇&#x200B;**Experience Manager**。
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page1.png)

1. 按一下Cloud Manager卡片中的&#x200B;**Launch**。 成功登入[!UICONTROL Cloud Manager]後，您就可以使用使用者介面(UI)了。
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/landing-page2.png)


## Cloud Manager登陸頁面 {#cloud-manager-landing}

成功登入後，系統會將您導向至Cloud Manager的登陸頁面。

>[!NOTE]
>根據在[!UICONTROL Cloud Manager]中指派的角色和應用程式的狀態，使用[!UICONTROL Cloud Manager] UI時會看到不同的畫面。

您會看到以下三個選項之一：

* **當Cloud Manager中沒有程式時**

   如果組織中沒有任何方案，您的登錄頁面會引導您建立第一個方案，如下圖所示。
   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin0.png)

* **當Cloud Manager中已存在程式時**

   如果方案已存在於您的組織中，則您的登錄頁面會引導您新增其他方案，並顯示您所有的現有方案，如下圖所示。

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

* **當程式存在且用戶是系統管理員時**

   如果您的組織中已存在程式，並且您是系統管理員，則您的登錄頁面將顯示&#x200B;**管理訪問**&#x200B;按鈕以及&#x200B;**添加程式**&#x200B;選項，如下圖所示。

   ![](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/admin-console-4.png)

在此處，具有權限的使用者（例如Cloud Manager中的業務擁有者角色）可以選取&#x200B;**新增程式**&#x200B;以啟動[新增程式精靈](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en#getting-access)。

若要了解如何在Cloud Manager中新增程式，請參閱：

* 建立生產計畫
* 建立沙箱方案