---
title: AEMas a Cloud Service團隊和產品配置檔案
description: 按照本頁瞭解有關AEMas a Cloud Service團隊和產品配置檔案。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: 56ca8e80081e62ceb3f5fc2bf9c32aa3bcee12c6
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# AEMas a Cloud Service團隊和產品配置檔案 {#product-profiles}

## 產品配置檔案 {#profiles}

在授予用戶對特定Adobe解決方案的訪問權限時，您不一定希望授予他們完全訪問權限。 「產品配置檔案」使每個解決方案都具有自己的一組用戶權限。 可通過 [Adobe Admin Console](/help/onboarding/learn-concepts/admin-console.md)。

閱讀有關 [AEMas a Cloud Service產品配置](#aem-product-profiles) 和 [Cloud Manager產品配置檔案](#cloud-manager-product-profiles) 瞭解在您的團隊設定時，這些工作如何協調進行。

## AEMas a Cloud Service產品配置檔案 {#aem-product-profiles}

AEMas a Cloud Service是完全雲本地的服務AEM。 它以AEM雲本機方式提供，並具有新屬性，如始終開啟、始終最新、始終安全且始終處於規模。 同時，它保留了作為可定製平台為客戶提AEM供的主要價值主張，並允許企業級團隊在其開發和交付過程中整合。 請參閱 [Adobe Experience Manager as a Cloud Service簡介](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en) 來瞭解更多AEMas a Cloud Service。

您AEM的as a Cloud Service團隊成員將在入職期間通過Admin Console添加並分配到以下一個或多個產品配置檔案。

* **管AEM理員**:通常AEM會將管理員分配給開發人員，特別是需要訪問開發環境的開發人員。 Administrators產AEM品配置檔案將用於授予關聯實例中的管理員AEM權限。

* **用AEM戶**:用AEM戶是您組織中使用as a Cloud Service作為AEM與Adobe協定的一部分的用戶。 這些成員需要訪問AEM以執行其任務。 用戶AEM產品配置檔案通常分配給創AEM建和審閱內容的內容作者(這可以是幾種類型；例如，頁面、資產、出版物等)，然後將其發佈到您的網站。 下面AEM顯示的用戶產品配置檔案已分配給這些成員。

   ![](/help/onboarding/learn-concepts/assets/admin-console-profiles.png)

   >[!NOTE]
   >分配給as a Cloud Service產品配AEM置檔案的每個用戶都具有（只讀）Cloud Manager訪問權限。

## Cloud Manager產品配置檔案 {#cloud-manager-product-profiles}

Cloud Manager具有預配置的產品配置檔案，或更簡單的基於角色的權限。 您的系統管理員將負責通過為這些產品配置檔案分配來設定您的雲管理器團隊，並且必須熟悉這些產品配置檔案以及要分配給哪些團隊成員。
>[!NOTE]
>請參閱 [雲管理器中基於角色的權限](/help/onboarding/learn-concepts/cloud-manager-introduction.md##role-based-permissions) 的子菜單。

每個產品配置檔案都具有與其關聯的特定權限。 例如，如果您的角色是：

* **業務所有者**，您有權添加新程式或編輯程式、添加或更新環境、添加/編輯/刪除管道並運行任何管道，以及將代碼部署到環境或代AEM碼質量。

* **部署管理器**，您具有添加或更新環境、運行任何管道以及將代碼部署到環境或代AEM碼質量的權限。

* **開發人員**，您有權生成訪問Git的個人訪問令牌。

* **程式管理器**，您有權調度管道、覆蓋3層質量門和提供生產批准。

用戶可以分配給多個產品配置檔案。 例如，將業務所有者和部署管理器角色分配給用戶時，會為用戶提供這些權限的組合或總和。

您的雲管理器團隊將至少包括：

* 一個業務所有者，通常也是系統管理員，並且必須是第一個登錄並訪問雲管理器的人
* 一個部署管理器
* 一個開發人員

   >[!NOTE]
   >要授予用戶對AEMas a Cloud Service的訪問權限，用戶必須屬於以下兩種產品配置檔案之一： `AEM Users` 或 `AEM Administrators`。 必須授予您對實例的權限，管理關聯雲管理器的權限將不足。
