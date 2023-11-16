---
title: AEM as a Cloud Service 團隊和產品設定檔
description: 了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授與和限制您的授權 Adobe 解決方案的存取權。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 96%

---


# AEM as a Cloud Service 團隊和產品設定檔 {#product-profiles}

了解 AEM as a Cloud Service 團隊和產品設定檔如何能夠授與和限制您的授權 Adobe 解決方案的存取權。

## 產品設定檔 {#profiles}

在授與使用者特定 Adobe 解決方案的存取權時，您不一定要授與他們完整的存取權。產品設定檔使每個解決方案都可以擁有自己的一組使用者權限。這些可透過 [Admin Console](/help/journey-onboarding/admin-console.md) 取得和存取。

## AEM as a Cloud Service 產品設定檔 {#aem-product-profiles}

AEM as a Cloud Service 是完全的雲端原生產品，可提供 AEM 即服務。它以雲端原生方式提供 AEM，具有永遠可用、永遠最新、永遠安全和永遠可擴展等新屬性。同時，它保留了 AEM 作為可自訂平台提供給客戶的主要價值主張，並允許企業級團隊整合到他們的開發和交付計畫中。若要深入了解 AEM as a Cloud Service，請參閱 [Adobe Experience Manager as a Cloud Service 簡介](/help/overview/introduction.md)。

在上線期間，您的 AEM as a Cloud Service 團隊成員會透過 Admin Console 新增並指派到以下一個或多個產品設定檔。

* **AEM管理員**：AEM管理員通常會指派給開發人員，特別是需要存取開發環境等的開發人員。 AEM 管理員的產品設定檔用於在關聯的 AEM 執行個體中授與管理員權限。

* **AEM 使用者**：AEM 使用者是您組織中使用 AEM as a Cloud Service 來建立內容的使用者。這些使用者需要存取AEM才能完成他們的工作。 AEM 使用者產品設定檔通常會指派給建立和檢閱內容的 AEM 內容作者。此內容可以是多種類型，例如頁面、資產、出版物等。以下顯示的 AEM 使用者產品設定檔已指派給這些成員。

![產品設定檔](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>指派給 AEM as a Cloud Service 產品設定檔的每個使用者透過&#x200B;**雲端管理員使用者**&#x200B;角色具有對 Cloud Manager 的唯讀存取權。
>
>唯具有&#x200B;**雲端管理員使用者**&#x200B;角色的使用者可以使用「**計畫**」選單選項，登入 Cloud Manager 並瀏覽至 AEM 編寫環境 (如果存在)。**雲端管理員使用者**&#x200B;角色不足以存取計畫詳細資料。如果需要此類存取權，系統管理員必須授予使用者其他角色。

>[!WARNING]
>
>**AEM 管理員**&#x200B;產品設定檔名稱不得變更。如果變更 **AEM 管理員**&#x200B;產品設定檔名稱，會將所有指派到該設定檔之使用者的管理員權限移除。

>[!TIP]
>
>* 若要深入了解 AEM 產品設定檔，請參閱[指派 AEM 產品設定檔](/help/journey-onboarding/assign-profiles-aem.md)。
>* 如需入門流程的詳細資訊，請參閱[上線歷程](/help/journey-onboarding/overview.md)

## Cloud Manager 產品設定檔 {#cloud-manager-product-profiles}

Cloud Manager 具有預先設定的產品設定檔，可以將其視為角色型權限。您的系統管理員負責將您的 Cloud Manager 團隊指派給這些產品設定檔來設定團隊。

>[!TIP]
>
>如需更多詳細資訊，請參閱[Cloud Manager 中的角色型權限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)。

每個產品設定檔都有與之關聯的特定權限。

* **業務負責人**
   * 在此角色中，您擁有權限可以新增方案或編輯方案、新增或更新環境、將程式碼部署到 AEM 環境或執行程式碼品質檢查。
   * 這類使用者會負責定義 KPI、核准生產部署並在必要時覆寫重要的 3 層級失敗。
* **部署管理員**
   * 在此角色中，您擁有權限可新增或更新環境、執行管道，和將程式碼部署到 AEM 環境或執行程式碼品質檢查。
   * 這類使用者會管理部署操作，並使用 Cloud Manager 來執行中繼/生產部署、編輯 CI/CD 管道、核准重要的 3 層級失敗 (如有必要)，並可存取 Git 存放庫。
* **開發人員**
   * 在此角色中，您擁有權限可產生個人存取權杖以存取 Git。
   * 這類使用者會開發和測試自訂應用程式，並主要使用 Cloud Manager 來檢視部署狀態，且可存取 Git 存放庫程式來認可程式碼。
* **方案管理員**
   * 在此角色中，您擁有權限可安排管道、覆寫 3 層品質門檻並提供生產核准。
   * 這類使用者會使用 Cloud Manager 來執行團隊設定、審查狀態、檢視 KPI，並可在必要時核准重要的 3 層級失敗。

可以將一個使用者指派給多個產品設定檔。例如，同時指派&#x200B;**業務負責人**&#x200B;和&#x200B;**部署管理員**&#x200B;角色以賦予使用者兩者的所有權限。

您的 Cloud Manager 團隊將至少包括：

* 一位&#x200B;**業務負責人**，他通常也是系統管理員，並且必須是第一個登入和存取 Cloud Manager 的人
* 一位&#x200B;**部署管理員**
* 一位&#x200B;**開發人員**

>[!NOTE]
>
>要取得AEM as a Cloud Service 的存取權，使用者必須屬於以下兩個產品設定檔之一：`AEM Users` 或 `AEM Administrators`。管理 Cloud Manager 的權限是不夠的。

>[!TIP]
>
>* 若要深入了解 Cloud Manager 產品設定檔，請參閱[將團隊成員指派到 Cloud Manager 產品設定檔](/help/journey-onboarding/assign-profiles-cloud-manager.md)。
>* 如需入門流程的詳細資訊，請參閱[上線歷程](/help/journey-onboarding/overview.md)。
