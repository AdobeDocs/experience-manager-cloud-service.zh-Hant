---
title: 了解參考示範附加元件安裝
description: 了解 Cloud Manager 以及如何使用它來安裝附加元件。
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: ht
source-wordcount: '941'
ht-degree: 100%

---

# 了解參考示範附加元件安裝 {#understand-installation}

了解 Cloud Manager 以及如何使用它來安裝附加元件。

>[!TIP]
>
>如果您熟悉 Cloud Manager 或想直接跳到附加元件的設定和使用，請跳至「[建立方案和管道](create-program.md)」。
>
>如果您想了解 Cloud Manager 和 AEM 如何搭配運作以建立示範環境，以及如何設定並使用您自己的環境，請繼續閱讀目前文件。

## 目標 {#objective}

本文件協助您了解參考示範附加元件的安裝流程如何運作，並說明不同部分如何搭配。閱讀文件後，您應該：

* 對 Cloud Manager 有基本的了解。
* 了解管道如何將內容和設定傳遞到 AEM。
* 了解如何透過數次點選即可建立預填示範內容的網站。

本文件著重介紹 AEM 參考示範附加元件的基本元素，讓您能繼續歷程的下一步並開始安裝。

雖然建議您繼續執行此歷程，如果您已經熟悉 Cloud Manager 或想直接跳到附加元件的設定和使用，請跳至「[建立方案和管道](create-program.md)」。

## 負責角色 {#responsible-role}

此歷程適用於您的組織中在 Cloud Manager 具有&#x200B;**業務負責人**&#x200B;角色的系統管理員。

## 要求和先決條件 {#requirements-prerequisites}

了解並開始使用參考示範附加元件有最低要求。

### 知識 {#knowledge}

* Cloud Manager 基本知識

### 工具 {#tools}

* 成為組織中具有&#x200B;**業務負責人**&#x200B;角色的一員

## 了解 Cloud Manager {#cloud-manager}

Cloud Manager 是 AEM as a Cloud Service 的重要元件，是使用平台的單一入口。

使用 Cloud Manager 來管理支援 AEM 專案的雲端資源，包括所需的環境和工具。針對本歷程的目的而言，您無需完全了解 Cloud Manager。但是，您必須熟悉一些基本概念。

>[!TIP]
>
>如果您想深入了解 Cloud Manager，請參閱本文章的「[其他資源](#additional-resources)」區段，內有多個連結提供更多資訊。

### 方案 {#programs}

當您登入雲端管理時，您可以存取一個或多個&#x200B;**方案**。一個項目可以用多種不同的方式來定義，但最容易將其視為與一個品牌識別相關的網站和體驗。

如果您代表 **WKND Travel and Adventure Enterprises** 登入 Cloud Manager，您可以建立 **WKND Nightlife** 方案以及 **WKND Backyard Projects** 方案。這兩個方案均可使用 AEM 環境管理相關的網站。

### 沙箱 {#sandboxes}

方案可以是生產方案或沙箱方案。

* **生產方案**&#x200B;建立的目的在於方案最終準備好上線時允許即時流量。
* **沙箱方案**&#x200B;是為培訓、執行示範、啟用功能、POC 等而建立，並未為了即時流量。

若要安裝 AEM 參考示範附加元件，請建立一個沙箱方案。

>[!NOTE]
>
>AEM 參考示範附加元件僅可在沙箱方案中使用。

## 安裝及使用流程 {#installation-flow}

現在您已經了解 Cloud Manager 的一些基本概念，AEM 參考示範附加元件的安裝在概念上變得簡單。

1. 登入 Cloud Manager。
1. 建立沙箱 AEM 方案，啟用 AEM 參考示範附加元件作為方案選項。
1. 示範內容和設定部署到方案中。示範內容包含：
   * 利用 AEM 功能建立各種 AEM 網站的網站範本，且預先填入最佳實務範例。
   * 用於管理示範內容的設定工具。
1. 在新沙箱方案中登入 AEM，使用快速建立網站工具並根據範本建立示範網站。
1. 使用設定工具來管理這些示範網站和範本，包括不需要時將其刪除。

## AEM 網站範本 {#site-templates}

AEM 網站範本是包含網站的預先定義內容和結構的套件。您可以自訂網站範本以滿足特定專案的需求，因此當 AEM 管理員建立網站時，他們可以選擇適用於其業務案例的範本。

AEM 參考示範附加元件包含多個範本，滿足各種測試和示範需求。建立方案並部署管道來安裝附加元件後，您可以登入 AEM 並根據許多示範範本來建立網站

## 下一步 {#what-is-next}

您已完成 AEM 參考示範附加元件歷程的這個部分，您應該：

* 對 Cloud Manager 有基本的了解。
* 了解管道如何將內容和設定傳遞到 AEM。
* 了解如何透過數次點選即可建立預填示範內容的網站。

以此知識為基礎並繼續您的 AEM 快速建立網站歷程，接著檢閱「[建立方案和管道](create-program.md)」，從中了解如何設定新方案和管理來部署附加元件。

## 其他資源 {#additional-resources}

因為我們建議您檢閱「[建立方案和管理](create-program.md)」並繼續快速建立網站歷程的下個部分，所以提供以下其他可用資源。這些資源深入探討本文件提及的概念。但是這並不是繼續執行歷程的必要條件。

* [了解方案和方案類型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/program-types.html) - 從這裡開始了解即時方案和沙箱方案之間的差異。
* [網站範本](/help/sites-cloud/administering/site-creation/site-templates.md) - 如果您想了解有關網站範本的結構以及如何使用它們建立網站的更多資訊，請參閱本文件。
* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/onboarding-concepts/cloud-manager-introduction.html) - 如果您想要 Cloud Manager 功能的更多詳細資訊，您可能想直接查閱深入的技術文件。
