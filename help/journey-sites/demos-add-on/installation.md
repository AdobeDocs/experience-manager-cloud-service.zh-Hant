---
title: 瞭解參考示範附加元件安裝
description: 了解 Cloud Manager 以及如何使用它來安裝附加元件。
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 6%

---

# 瞭解參考示範附加元件安裝 {#understand-installation}

了解 Cloud Manager 以及如何使用它來安裝附加元件。

>[!TIP]
>
>如果您有使用Cloud Manager的經驗，或想直接跳至附加元件的設定和使用，請跳至 [建立計畫和管道](create-program.md)
>
>如果您想瞭解Cloud Manager和AEM如何合作來建立您的示範環境，以及如何設定和使用您自己的環境，請繼續閱讀目前的檔案。

## 目標 {#objective}

本檔案可協助您瞭解「參考示範」附加元件的安裝程式如何運作，說明不同部分如何共同運作。 閱讀本檔案後，您應該：

* 基本瞭解Cloud Manager。
* 瞭解管道如何將內容和設定傳送至AEM。
* 瞭解範本如何按幾下即可建立已預先填入示範內容的網站。

在繼續此歷程的下一步來開始安裝之前，本檔案著重於瞭解AEM參考示範附加元件的這些基本片段。

雖然我們建議您繼續此歷程，但如果您已體驗Cloud Manager，或想直接跳至設定和附加元件的使用，請跳至 [建立計畫和管道](create-program.md).

## 負責角色 {#responsible-role}

此歷程適用於身為 **業務負責人** 在您組織的Cloud Manager中的角色。

## 要求和先決條件 {#requirements-prerequisites}

只需達到最低需求，即可瞭解並開始使用參考示範附加元件。

### 知識 {#knowledge}

* Cloud Manager的基本知識

### 工具 {#tools}

* 成為以下專案的成員： **業務負責人** 您組織的Cloud Manager中的角色

## 瞭解Cloud Manager {#cloud-manager}

Cloud Manager是AEMas a Cloud Service的必要元件，可作為平台的單一入口點。

Cloud Manager用於管理支援您的AEM專案的雲端資源，包括所需的環境和工具。 在此歷程中，不需要完全瞭解Cloud Manager。 不過，您必須熟悉一些基本概念。

>[!TIP]
>
>如果您想深入瞭解Cloud Manager，請參閱 [其他資源](#additional-resources) 章節，以取得更多資訊的連結。

### 方案 {#programs}

登入Cloud Manager時，您可以存取一或多個 **計畫**. 雖然可以透過許多不同方式定義程式，但最簡單的做法是將其視為與某個品牌身分識別相關聯的網站和體驗相關聯。

如果您登入Cloud Manager，表示 **WKND旅遊和冒險企業**，您可以建立 **WKND Nightlife** 方案與 **WKND後院專案** 程式。 這兩個計畫都會有AEM環境來管理其關聯的網站。

### 沙箱 {#sandboxes}

程式可以是生產程式或沙箱程式。

* **生產計畫** 建立以便在您的方案準備好上線時最終允許上線流量。
* **沙箱計畫** 專為訓練、執行示範、訓練、POC等而建立，不適用於即時流量。

若要安裝AEM參考示範附加元件，請建立沙箱計畫。

>[!NOTE]
>
>AEM參考示範附加元件僅適用於沙箱計畫。

## 安裝和使用流程 {#installation-flow}

現在您已瞭解Cloud Manager的一些基本概念，從概念上來說，AEM參考示範附加元件的安裝很簡單。

1. 登入Cloud Manager。
1. 建立沙箱AEM計畫，啟動AEM參考示範附加元件作為計畫的選項。
1. 示範內容和設定已部署至程式。 示範內容包含：
   * 用來使用AEM功能建立各種AEM網站的網站範本，預先填入最佳實務範例。
   * 管理示範內容的設定工具。
1. 在您的新沙箱計畫中登入AEM，使用快速網站建立工具並根據範本建立示範網站。
1. 使用設定工具管理這些示範網站和範本，包括不再需要時將其刪除。

## AEM網站範本 {#site-templates}

AEM網站範本是包含網站預先定義之內容和結構的套件。 可自訂網站範本以符合特定專案的需求，以便當AEM管理員建立網站時，可以從適用於其業務案例的範本中進行選擇。

AEM參考示範附加元件包含多個範本，可滿足各種測試和示範需求。 建立方案並部署管道以安裝附加元件後，您可以登入AEM並根據許多示範範本建立網站

## 下一步 {#what-is-next}

現在您已完成AEM參考示範附加元件歷程的這一部分，您應：

* 基本瞭解Cloud Manager。
* 瞭解管道如何將內容和設定傳送至AEM。
* 瞭解範本如何按幾下即可建立已預先填入示範內容的網站。

在此知識的基礎上繼續您的AEM快速網站建立歷程，方法是檢閱 [建立計畫和管道，](create-program.md) 在這裡，您可以瞭解如何設定新計畫和管道以部署附加元件。

## 其他資源 {#additional-resources}

我們建議您檢閱以下資訊，以前往快速網站建立歷程的下一部分 [建立計畫和管道](create-program.md)下，以下是一些其他選用的資源。 這些資源會更深入地探討本檔案中提及的概念。 但是，他們不需要繼續歷程。

* [瞭解方案和方案型別](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/programs/program-types.html)  — 從這裡開始瞭解即時和沙箱計畫之間的差異。
* [網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)  — 如果您想進一步瞭解網站範本的結構，以及如何使用它們來建立網站，請參閱本檔案。
* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/onboarding-concepts/cloud-manager-introduction.html) - 如果您想要 Cloud Manager 功能的更多詳細資訊，您可能想要直接查閱深入的技術文件。
