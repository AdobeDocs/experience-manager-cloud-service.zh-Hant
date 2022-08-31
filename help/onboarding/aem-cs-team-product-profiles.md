---
title: AEMas a Cloud Service團隊和產品配置檔案
description: 瞭解AEMas a Cloud Service團隊和產品配置檔案以及授予和限制對許可Adobe解決方案的訪問。
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
source-git-commit: d54c25791cbb06232ff6e24bb7b8005b366a2144
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# AEMas a Cloud Service團隊和產品配置檔案 {#product-profiles}

瞭解AEMas a Cloud Service團隊和產品配置檔案以及授予和限制對許可Adobe解決方案的訪問。

## 產品配置檔案 {#profiles}

在授予用戶對特定Adobe解決方案的訪問權限時，您不一定希望授予他們完全訪問權限。 產品配置檔案使每個解決方案都擁有自己的一組用戶權限。 可通過 [Admin Console。](/help/journey-onboarding/admin-console.md)

## AEMas a Cloud Service產品配置檔案 {#aem-product-profiles}

AEMas a Cloud Service是完全以雲為本的服務AEM。 它以AEM雲本機方式提供，並具有新屬性，如始終開啟、始終最新、始終安全且始終處於規模。 同時，它保留了作為可定製平台為客戶提AEM供的主要價值主張，並允許企業級團隊在其開發和交付過程中整合。 請參閱 [Adobe Experience Manager as a Cloud Service簡介](/help/overview/introduction.md) 來瞭解更多AEMas a Cloud Service。

您AEM的as a Cloud Service團隊成員將在入職期間通過Admin Console添加並分配到以下一個或多個產品配置檔案。

* **管AEM理員**:通AEM常將管理員指派給需要訪問例如開發環境的開發人員。 管理AEM員的產品配置檔案將用於授予關聯實例中的管理員AEM權限。

* **用AEM戶**:用AEM戶是您組織中通常使用AEMas a Cloud Service建立內容的用戶。 這些用戶需要訪問AEM才能執行其任務。 用戶AEM產品配置檔案通常分配給創AEM建和審閱內容的內容作者。 此內容可以有多種類型，如頁面、資產、出版物等。 下面AEM所示的用戶產品配置檔案已分配給這些成員。

![產品配置檔案](/help/onboarding/assets/admin-console-profiles.png)

>[!NOTE]
>
>分配給as a Cloud Service產品配AEM置檔案的每個用戶都具有（只讀）Cloud Manager訪問權限。

>[!TIP]
>
>有關登機過程的詳細資訊，請參閱 [登機之旅。](/help/journey-onboarding/overview.md)

## Cloud Manager產品配置檔案 {#cloud-manager-product-profiles}

Cloud Manager具有預配置的產品配置檔案，可以將其視為基於角色的權限。 您的系統管理員負責通過將Cloud Manager團隊分配給這些產品配置檔案來設定這些團隊。

>[!TIP]
>
>請參閱文檔 [雲管理器中基於角色的權限](/help/onboarding/cloud-manager-introduction.md#role-based-permissions) 的子菜單。

每個產品配置檔案都具有與它們關聯的特定權限。

* **業務所有者**  — 在此角色中，您有權添加新程式或編輯程式、添加或更新環境、將代碼部署到環境AEM或執行代碼質量檢查。
* **部署管理器**  — 在此角色中，您具有添加或更新環境、運行任何管道以及將代碼部署到環境或執AEM行代碼質量檢查的權限。
* **開發人員**  — 在此角色中，您具有生成個人訪問令牌以訪問Git的權限。
* **程式管理器**  — 在此角色中，您有權安排管道、覆蓋3層質量門並提供生產批准。

用戶可以分配給多個產品配置檔案。 例如，分配兩者 **業務所有者** 和 **部署管理** r角色為用戶提供這些權限的總和。

您的雲管理器團隊將至少包括：

* 一 **業務所有者**，通常也是系統管理員，並且必須是第一個登錄並訪問Cloud Manager的人
* 一 **部署管理器**
* 一 **開發人員**

>[!NOTE]
>
>要授予用戶對AEMas a Cloud Service的訪問權限，用戶必須屬於以下兩種產品配置檔案之一： `AEM Users` 或 `AEM Administrators`。 管理雲管理器的權限不足。
