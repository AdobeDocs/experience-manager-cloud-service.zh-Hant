---
title: AEMas a Cloud Service團隊和產品設定檔
description: 了解AEMas a Cloud Service團隊和產品設定檔，以及如何授與和限制您授權Adobe解決方案的存取權。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: d54c25791cbb06232ff6e24bb7b8005b366a2144
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# AEMas a Cloud Service團隊和產品設定檔 {#product-profiles}

了解AEMas a Cloud Service團隊和產品設定檔，以及如何授與和限制您授權Adobe解決方案的存取權。

## 產品設定檔 {#profiles}

授與使用者特定Adobe解決方案的存取權時，您不一定想授予他們完整存取權。 產品設定檔可讓每個解決方案擁有其專屬的一組使用者權限。 這些功能可透過 [Admin Console。](/help/journey-onboarding/admin-console.md)

## AEMas a Cloud Service產品設定檔 {#aem-product-profiles}

AEM as a Cloud Service是完全雲端原生的產品，可提供AEM as a service。 它以雲端原生方式提供AEM，並提供新屬性，例如永遠開啟、隨時最新、一律安全且隨時可擴充。 同時，它保留了AEM作為可自訂平台提供給客戶的主要價值主張，並允許企業級團隊整合到其開發和交付過程中。 請參閱 [Adobe Experience Manager as a Cloud Service簡介](/help/overview/introduction.md) 深入了解AEMas a Cloud Service。

您的AEMas a Cloud Service團隊成員將在上線期間，透過Admin Console新增並指派給下列一或多個產品設定檔。

* **AEM管理員**:通常會將AEM管理員指派給開發人員，尤其是需要存取開發環境的開發人員。 AEM管理員的產品設定檔將用來授予相關AEM例項的管理員權限。

* **AEM使用者**:AEM使用者是貴組織中一般使用AEMas a Cloud Service來建立內容的使用者。 這些使用者需要存取AEM才能執行其工作。 通常會將AEM使用者產品設定檔指派給建立及檢閱內容的AEM內容作者。 此內容可能有許多類型，例如頁面、資產、出版物等。 系統會將以下所示的AEM使用者產品設定檔指派給這些成員。

![產品設定檔](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>指派給AEMas a Cloud Service產品設定檔的每位使用者都擁有Cloud Manager的（唯讀）存取權。

>[!TIP]
>
>如需上線程式的詳細資訊，請參閱 [入門歷程。](/help/journey-onboarding/overview.md)

## Cloud Manager產品設定檔 {#cloud-manager-product-profiles}

Cloud Manager已預先設定產品設定檔，可視為角色型權限。 您的系統管理員負責將Cloud Manager團隊指派給這些產品設定檔，以便進行設定。

>[!TIP]
>
>請參閱該文檔 [Cloud Manager中的角色型權限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) 以取得更多詳細資訊。

每個產品設定檔都有與其相關聯的特定權限。

* **業務負責人**  — 在此角色中，您有權添加新程式或編輯程式、添加或更新環境、將代碼部署到AEM環境，或執行代碼質量檢查。
* **部署管理員**  — 在此角色中，您有權新增或更新環境、執行任何管道，以及將程式碼部署至AEM環境，或執行程式碼品質檢查。
* **開發人員**  — 在此角色中，您有權產生個人存取權杖以存取Git。
* **計畫經理**  — 在此角色中，您有權調度管道、覆蓋3層質量門並提供生產批准。

可將使用者指派給多個產品設定檔。 例如，指派兩者 **業務負責人** 和 **部署管理**&#x200B;或角色給使用者可提供這些權限的總和。

您的Cloud Manager團隊將至少包含：

* 一 **業務負責人**，通常也是系統管理員，且必須是第一個登入及存取Cloud Manager的人員
* 一 **部署管理員**
* 一 **開發人員**

>[!NOTE]
>
>若要授與AEM as a Cloud Service的存取權，使用者必須屬於下列兩個產品設定檔之一： `AEM Users` 或 `AEM Administrators`. 管理Cloud Manager的權限不足。
