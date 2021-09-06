---
title: AEM as a Cloud Service團隊和產品設定檔
description: 請詳閱本頁面，了解AEM as a Product Team and Product Profiles。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 56ca8e80081e62ceb3f5fc2bf9c32aa3bcee12c6
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# AEM as a Cloud Service團隊和產品設定檔 {#product-profiles}

## 產品設定檔 {#profiles}

授與使用者特定Adobe解決方案的存取權時，您不一定想授予他們完整存取權。 產品設定檔可讓每個解決方案擁有自己的一組使用者權限。 這些檔案可透過[Adobe Admin Console](/help/onboarding/learn-concepts/admin-console.md)取得。

深入了解[AEM as a Cloud Service產品設定檔](#aem-product-profiles)和[Cloud Manager產品設定檔](#cloud-manager-product-profiles)，以了解在您的團隊設定時，這些設定檔如何搭配運作。

## AEM as a Cloud Service產品設定檔 {#aem-product-profiles}

AEM as aCloud Service是提供AEM as a service的完全雲端原生產品。 它以雲端原生方式提供AEM，並提供新屬性，例如永遠開啟、隨時最新、一律安全且隨時可擴充。 同時，它保留了AEM作為可自訂平台提供給客戶的主要價值主張，並允許企業級團隊整合到其開發和交付過程中。 請參閱[Adobe Experience Manager as aCloud Service簡介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en)以深入了解AEM as aCloud Service。

您的AEM作為Cloud Service團隊成員將會在上線期間，透過Admin Console新增並指派給下列一或多個產品設定檔。

* **AEM管理員**:通常會將AEM管理員指派給開發人員，尤其是需要存取開發環境的開發人員。AEM管理員產品設定檔將用來授予相關聯AEM例項的管理員權限。

* **AEM使用者**:AEM使用者是貴組織中使用AEM作為Cloud Service，並與Adobe簽訂合約的使用者。這些成員需要存取AEM才能執行其工作。 AEM使用者產品設定檔通常會指派給建立及檢閱內容的AEM內容作者(這可以是數種類型；例如頁面、資產、出版物等)，再發佈到您的網站。 系統會將下列AEM使用者產品設定檔指派給這些成員。

   ![](/help/onboarding/learn-concepts/assets/admin-console-profiles.png)

   >[!NOTE]
   >指派給AEM作為Cloud Service產品設定檔的每位使用者都擁有Cloud Manager的（唯讀）存取權。

## Cloud Manager產品設定檔 {#cloud-manager-product-profiles}

Cloud Manager已預先設定產品設定檔，或更簡單的角色型權限。 系統管理員將指派給這些產品設定檔，負責設定您的Cloud Manager團隊，且必須熟悉這些產品設定檔，以及要指派給哪些團隊成員。
>[!NOTE]
>如需詳細資訊，請參閱Cloud Manager](/help/onboarding/learn-concepts/cloud-manager-introduction.md##role-based-permissions)中的[角色型權限。

每個產品設定檔都有與其相關聯的特定權限。 例如，如果您的角色為：

* **業務擁有者**，您就擁有新增程式或編輯程式、新增或更新環境、新增/編輯/刪除管道和執行任何管道，以及將程式碼部署至AEM環境或程式碼品質的權限。

* **部署管理員**，則您有權新增或更新環境、執行任何管道，以及將程式碼部署至AEM環境或程式碼品質。

* **開發人員**，您便有權產生個人存取權杖以存取Git。

* **計畫管理員**，您有權計畫管道、覆蓋3層質量門並提供生產批准。

可將使用者指派給多個產品設定檔。 例如，將業務所有者和部署管理器角色分配給用戶時，會為其提供這些權限的組合或總和。

您的Cloud Manager團隊將至少包含：

* 一個業務所有者（通常也是系統管理員）必須是登錄和訪問Cloud Manager的第一個人
* 一個部署管理員
* 一位開發人員

   >[!NOTE]
   >若要授與AEM as aCloud Service的存取權，使用者必須屬於下列兩個產品設定檔之一：`AEM Users`或`AEM Administrators`。 您必須獲得執行個體的權限，但管理相關Cloud Manager的權限是不夠的。
